<template>
  <v-container fluid class="d-flex flex-column align-center">
    <div id="viz" />
    <v-btn @click="changeData">Change Data</v-btn>
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
  mounted() {
    this.createViz()
  },
  methods: {
    createViz() {
      let tempColor = ''

      const yScale2 = d3
      .scaleLinear()
      .domain([0, d3.max(this.barData)])
      .range([0, this.height])

      const xScale2 = d3.scaleBand()
        .domain(this.barData)
        .paddingInner(.3)
        .paddingOuter(.1)
        .range([0, this.width])

      const colors2 = d3.scaleLinear()
        .domain([0, this.barData.length * .33, this.barData.length * .66, this.barData.length])
        .range(['#b58929', '#c61c6f', '#268bd2', '#85992c'])

      const myChart = d3
        .select('#viz')
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
          .attr('height', 0)
          .attr('y', this.height)
          
          .attr('x', (d) => {
            return xScale2(d)
          })
          
          .on('mouseover', function (d, i) {
            tempColor = this.style.fill
            d3.select(this)
              .style('fill', '#FFFF00')
          })
          .on('mouseout', function (d, i) {
            d3.select(this)
              .style('fill', tempColor)
          })


        myChart.transition()
          .attr('height', function (d) {
            return yScale2(d)
          })
          .attr('y', (d) => {
            return this.height - yScale2(d)
          })
          .delay((d,i) => {
            return i * 20
          })
          .duration(1000)
          .ease(d3.easeBounceOut)
    },
    changeData() {
      this.barData = []
      for(let i = 0; i < Math.random() * 100; i++) {
        this.barData.push(Math.random() * 30)
      }
      console.log('DATA', this.data);
      d3
        .select('#viz svg').remove('svg')
      this.createViz()
    }
  }
}
</script>

<style>

</style>