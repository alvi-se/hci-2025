<script setup lang="ts">

import { onMounted, onBeforeUnmount, ref } from 'vue';
import maplibregl from 'maplibre-gl';
import 'maplibre-gl/dist/maplibre-gl.css';
import { MapboxOverlay } from '@deck.gl/mapbox';
import { HexagonLayer } from '@deck.gl/aggregation-layers';
import Papa from 'papaparse';

interface CsvData {
  lat: number;
  lon: number;
}

// Reference to HTML container
const mapContainer = ref<HTMLDivElement | null>(null);
let mapInstance: maplibregl.Map | null = null;
let deckOverlay: MapboxOverlay | null = null;

// static CSV file (public folder)
const CSV_PATH = '/data.csv';

onMounted(() => {
  // Download data when component has been created in page
  Papa.parse(CSV_PATH, {
    download: true,
    header: true,
    dynamicTyping: true,
    skipEmptyLines: true,
    complete: (results) => {
      const data = results.data as CsvData[];
      console.log(`Obtained ${data.length} rows`)
      initMap(data);
    },
    error: (err) => {
      console.error("Errore lettura CSV:", err);
    }
  });
});

function initMap(data: CsvData[]) {
  if (!mapContainer.value) return;

  // Instantiate map
  mapInstance = new maplibregl.Map({
    container: mapContainer.value,
    // Positron style by CartoDB
    style: 'https://basemaps.cartocdn.com/gl/positron-gl-style/style.json',
    center: [34.86, 31.59], // Palestine
    zoom: 7,
    pitch: 45, // Tilt map
    bearing: 0,
  });

  deckOverlay = new MapboxOverlay({
    layers: [
      /*
      This is really ugly, I'm commenting it out temporarily

      // Palestine layer
      new GeoJsonLayer({
        id: "Palestine",
        data: "/palestine.geojson",
        getFillColor: [0, 0, 0, 0],
        getLineColor: [0x0, 0xff, 0x0, 0xff],
        lineWidthMinPixels: 5,
        getPolygonOffset: () => [1, 1],
      }),
      // Israel layer
      new GeoJsonLayer({
        id: "Israel",
        data: "/israel.geojson",
        getFillColor: [0, 0, 0, 0],
        getLineColor: [0xff, 0x0, 0x0, 0xff],
        lineWidthMinPixels: 5,
        getPolygonOffset: () => [1, 1],
      }),
      */
      // Casualties layer
      new HexagonLayer<CsvData>({
        id: 'casualties',
        data: data,
        pickable: true,
        extruded: true, // Enable 3D height
        radius: 4000,   // Hexagon radius in meters
        elevationScale: 100, // Height factor
        gpuAggregation: true,

        getPosition: (d: CsvData) => [d.lon, d.lat],

        colorRange: [
          [1, 152, 189],
          [73, 227, 206],
          [216, 254, 181],
          [254, 237, 177],
          [254, 173, 84],
          [209, 55, 78]
        ],
      }),
    ]
  });

  // Deck.gl map controller
  mapInstance.addControl(deckOverlay as any);
}

onBeforeUnmount(() => {
  if (mapInstance) mapInstance.remove();
});

</script>

<template>
  <div class="container">
    <div ref="mapContainer" class="map-container"></div>
  </div>
</template>

<style scoped>
.container {
  position: relative;
  width: 100%;
  height: 100vh;
}

.map-container {
  height: 100%;
}
</style>
