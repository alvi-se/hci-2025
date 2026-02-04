<script setup lang="ts">
import MapHexBin from './MapHexBin.vue';


</script>



<template>
  <main class="container">
    <h1>Web Visualizations</h1>
    <section>
      <h2>3D Hexbing Map</h2>
      
      <MapHexBin></MapHexBin>
      <p>This 3D Hexbin Map visualizes the geographic distribution of casualties in Palestine and Israel. The height of each hexagon represents the number of casualties in that area. The map reveals that the Gaza Strip has a higher density of casualties compared to the West Bank, with more casualties near the West Bank borders with Israel than in internal areas or borders with Jordan.</p>

      <h2>Demographics Exploration</h2>
      <p>This radial hierarchical tree visualizes victim records by citizenship, age, gender, and type of injury. The tree is color-coded by citizenship and allows interactive exploration of the data.</p>
      <iframe src="https://public.flourish.studio/visualisation/27352225/" width="100%" height="600px"></iframe>
      <p><strong>Gained Knowledge:</strong> The death tolls are not equally distributed across citizenship groups, with more records concentrated on the Palestinian side. The most deaths for both sides are for men between 20-30 years and by gunfire.</p>
    </section>
    <section>
      <h2>Beeswarm Chart</h2>
      <p>This interactive beeswarm plot shows the distribution of deaths over time and across age groups. Each point represents an individual, with color coding by citizenship and shape by location.</p>
      <iframe src="https://public.flourish.studio/visualisation/27126509/" width="100%" height="600px"></iframe>
      <p><strong>Gained Knowledge:</strong> Most events involve young to middle-aged individuals, with a strong imbalance across citizenships, and Palestinian individuals appearing most frequently.</p>
    </section>
    <section>
      <h2>Sankey Diagram mapping place of death to place of residence</h2>
      <p>This Sankey diagram maps the place of death to the place of residence, with flow widths representing the number of individuals and colors distinguishing districts.</p>
      <iframe src="https://public.flourish.studio/visualisation/27205389/" width="100%" height="600px"></iframe>
      <p><strong>Gained Knowledge:</strong> Many individuals die in their district of residence, but a substantial number die outside it, indicating cross-district movement.</p>
    </section>
    <section>
      <h2>Casualties by District and Two-Year Period</h2>
      <p>This pictogram compares casualty counts across districts and two-year periods, with each circle representing 10 casualties and color-coded by time period.</p>
      <iframe src="https://public.flourish.studio/visualisation/27382745/" width="100%" height="600px"></iframe>
      <p><strong>Gained Knowledge:</strong> The casualties are majorly concentrated in the locations of the North West Bank followed by the South West Bank, and for the time period between 2023-2024.</p>
    </section>
    <section>
      <h2>Snakey Diagram representing who killed who</h2>
      <p>This Sankey diagram shows the flow of casualties from victim groups to aggressor groups, with equal-width flows to emphasize relationship patterns.</p>
      <iframe src="https://public.flourish.studio/visualisation/27445631/" width="100%" height="600px"></iframe>
      <p><strong>Gained Knowledge:</strong> Palestinians faced the most diverse range of aggressors, while Jordanians were killed by only one type.</p>
    </section>
  </main>
</template>
