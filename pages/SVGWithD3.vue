<template>
  <v-container fluid class="d-flex flex-column fill-height">
    <h1>SVG with D3</h1>
    <div id="viz" />
  </v-container>
</template>

<script>
import * as d3 from 'd3'
export default {
  mounted () {
    d3.select('#viz')
      .append('svg')
        .attr('width', 600)
        .attr('height', 400)
        .style('background', 'green')

      .append('rect')
        .attr('x', 200)
        .attr('y', 100)
        .attr('height', 200)
        .attr('width', 200)
        .style('fill', 'yellow')
  }
}
</script>

<style>

</style>