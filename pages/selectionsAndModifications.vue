<template>
  <v-container fluid class="fill-height d-flex flex-column align-start">
    <h1 style="align-self: center">Selections and Modifications</h1>

    <h3 class="mt-6">Dogs</h3>
    <ul class="animal dogs">
      <li>German Shephard</li>
    </ul>

    <h3 class="mt-5">Fish</h3>
    <ul class="animal fish">
    </ul>

    <h4>Cars</h4>
    <ul class="cars">
      <li class="car"><span>Honda</span></li>
      <li class="car"><span>Ferrari</span></li>
    </ul>

    <input type="text" />
  </v-container>
</template>

<script>
import * as d3 from 'd3'
export default {
  mounted () {
    d3.select('.dogs')
      .append('li')
      .text('Golden Retriever')
      .remove('li')

    d3.selectAll('.animal')
      .insert('li')
      .html('Dogfish')
      .style('color', 'red')
      .style('font-size', '20px')
      .style('font-weight', 'bold')
      .append('span')
      .text(' 🐕🐟')

    d3.select('h1')
      .classed('blue', true)  // toggle custom classes
      .classed('text-h3 green--text', true)  // Toggle Vuetify classes

    d3.selectAll('.cars .car')
      .insert('span', ':first-child')  // insert before element
      .text('🚘 ')

    d3.select('input')
      .style('background-color', 'white')
      .style('border-radius', '20px')
      .style('padding', '0 15px')
      .classed('mt-3 mx-auto', true)
      .attr('type', 'password')
      .property('placeholder', 'Password')

  }
}
</script>

<style>
  .blue {
    color: blue;
  }

  .v-application .blue {
    background-color: transparent !important;
  }
</style>