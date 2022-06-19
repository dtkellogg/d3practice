<template>
  <v-container fluid class="fill-height d-flex flex-column" style="background: #404040">
    <h1>Bar Graphs</h1>
  <div id="viz" />
  <div id="viz2" class="mt-7" />
  <div id="viz3" class="mt-7" />
  </v-container>
</template>

<script>
import * as d3 from 'd3'
export default {
  data() {
    return {
      height: 400,
      width: 600,
      barWidth: 50,
      barOffset: 5,
      barData: [20, 30, 45, 15, 60, 23],
    }
  },
  mounted () {
    //
    // Just a basic bar chart:
    d3
      .select('#viz')
        .append('svg')
        .attr('width', this.width)
        .attr('height', this.height)
        .style('background', 'grey')

      .selectAll('rect')
        .data(this.barData)
        .enter().append('rect')
        .style('fill', 'red')
        .attr('width', this.barWidth)
        .attr('height', function (d) {
          return d
        })
        .attr('x', (d, i) => {
          return i * (this.barWidth + this.barOffset)
        })
        .attr('y', (d) => {
          return this.height - d
        })

    //
    // bar chart with x and y scaled. Y uses a linear scale and X uses an ordinal scale
    const yScale = d3
      .scaleLinear()
      .domain([0, d3.max(this.barData)])
      .range([0, this.height])

    const xScale = d3.scaleBand()
      .domain(this.barData)
      .paddingInner(.3)
      .paddingOuter(.1)
      .range([0, this.width])

    // Colors are based on height: the shorter the bar is, the more it goes towards #ffb832
    const colors = d3.scaleLinear()
      .domain([0, d3.max(this.barData)])
      .range(['#ffb832', '#c61c6f'])

    d3
      .select('#viz2')
        .append('svg')
        .attr('width', this.width)
        .attr('height', this.height)
        .style('background', 'grey')

      .selectAll('rect')
        .data(this.barData)
        .enter().append('rect')
        .style('fill', (d) => {
          return colors(d)
        })
        .attr('width', (d) => {
          return xScale.bandwidth()
        })
        .attr('height', function (d) {
          return yScale(d)
        })
        .attr('x', (d) => {
          return xScale(d)
        })
        .attr('y', (d) => {
          return this.height - yScale(d)
        })


    //
    // Fun Colors
    this.barData = []
      for(let i = 0; i < 100; i++) {
        this.barData.push(Math.random() * 30)
      }
    const yScale2 = d3
      .scaleLinear()
      .domain([0, d3.max(this.barData)])
      .range([0, this.height])

    const xScale2 = d3.scaleBand()
      .domain(this.barData)
      .paddingInner(.3)
      .paddingOuter(.1)
      .range([0, this.width])

    // Colors are based on height: the shorter the bar is, the more it goes towards #ffb832
    const colors2 = d3.scaleLinear()
      .domain([0, this.barData.length * .33, this.barData.length * .66, this.barData.length])
      .range(['#b58929', '#c61c6f', '#268bd2', '#85992c'])

    d3
      .select('#viz3')
        .append('svg')
        .attr('width', this.width)
        .attr('height', this.height)
        .style('background', 'grey')

      .selectAll('rect')
        .data(this.barData)
        .enter().append('rect')
        .style('fill', (d, i) => {
          return colors2(i)  // Make color inputs the indicies
        })
        .attr('width', (d) => {
          return xScale2.bandwidth()
        })
        .attr('height', function (d) {
          return yScale2(d)
        })
        .attr('x', (d) => {
          return xScale2(d)
        })
        .attr('y', (d) => {
          return this.height - yScale2(d)
        })

  }
}
</script>

<style>

</style>