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
      margin: {top: 20, left: 20, right: 0, bottom: 5},
      barWidth: 50,
      barOffset: 5,
      barData: [20, 30, 45, 15, 60, 23],
      dates: [
        new Date('Sun May 30 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun Jun 1 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun Jun 2 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun Jun 3 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun Jun 4 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun Jun 5 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun Jun 6 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun Jun 7 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun Jun 8 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun Jun 9 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun Jun 10 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun Jun 11 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun Jun 12 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun Jun 13 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun Jun 14 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun Jun 15 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun Jun 16 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun Jun 17 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun Jun 18 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun Jun 19 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun Jun 20 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun Jun 21 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun Jun 22 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun Jun 23 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun Jun 24 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun Jun 25 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun Jun 26 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun Jun 27 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun Jun 28 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun Jun 29 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun Jun 30 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun July 1 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun July 2 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun July 3 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun July 4 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun July 5 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun July 6 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun July 7 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun July 8 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun July 9 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun July 10 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun July 11 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun July 12 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun July 13 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun July 14 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun July 15 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun July 16 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun July 17 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun July 18 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun July 19 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun July 20 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun July 21 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun July 22 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun July 23 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun July 24 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun July 25 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun July 26 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun July 27 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun July 28 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun July 29 2022 13:51:16 GMT-0700 (Pacific Daylight Time)'),
        new Date('Sun July 30 2022 13:51:16 GMT-0700 (Pacific Daylight Time)')
      ]
    }
  },
  mounted() {
    console.log();
    this.height = 400 - this.margin.top - this.margin.bottom  // Creating margins
    this.width = 600 - this.margin.left - this.margin.right
    this.createViz()
  },
  methods: {
    createViz() {
      
      let tempColor = ''

      const yScale = d3.scaleLinear()
        .domain([0, d3.max(this.barData)])
        .range([0, this.height])

      // define yAxis and yAxis Ticks
      const yAxisValues = d3.scaleLinear()
        .domain([0, d3.max(this.barData)])
        .range([this.height, 0])

      const yAxisTicks = d3.axisLeft(yAxisValues)
        .ticks(10)  // this is how many ticks

      const xScale = d3.scaleBand()
        .domain(this.barData)
        .paddingInner(.3)
        .paddingOuter(.1)
        .range([0, this.width])

      const xAxisValues = d3.scaleTime()
        .domain([this.dates[0], this.dates[this.dates.length - 1]])
        .range([0, this.width])

      const xAxisTicks = d3.axisBottom(xAxisValues)
        // .ticks(d3.timeDay.every(1))  // One tick for every day
        .ticks(d3.timeWeek.every(1))  // One tick for every week
        // .ticks(d3.timeMonth.every(1))  // One tick for every month
        // .ticks(d3.timeYear.every(1))  // One tick for every month

      const colors = d3.scaleLinear()
        .domain([0, this.barData.length * .33, this.barData.length * .66, this.barData.length])
        .range(['#b58929', '#c61c6f', '#268bd2', '#85992c'])

      const myChart = d3
        .select('#viz')
          .append('svg')
          .attr('width', this.width + this.margin.left + this.margin.right)  // creating margins
          .attr('height', this.height + this.margin.top + this.margin.bottom)
          .style('background', 'grey')
          .append('g')   

          // Creating a margin
          .attr('transform', 'translate(' + this.margin.left + ',' + this.margin.right + ')')

        .selectAll('rect')
          .data(this.barData)
          .enter().append('rect')
          .style('fill', (d, i) => {
            return colors(i)
          })
          .attr('width', (d) => {
            return xScale.bandwidth()
          })
          .attr('height', 0)
          .attr('y', this.height)
          
          .attr('x', (d) => {
            return xScale(d)
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


        // yGuide
        d3.select('#viz svg').append('g')
          .attr('transform', 'translate(20,0)')
          .call(yAxisTicks)

        // xGuide
        d3.select('#viz svg').append('g')
          .attr('transform', 'translate(20,' + this.height + ')')
          .call(xAxisTicks)


        myChart.transition()
          .attr('height', function (d) {
            return yScale(d)
          })
          .attr('y', (d) => {
            return this.height - yScale(d)
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
        this.barData.push(Math.random() * 10)
      }
      d3.select('#viz svg').remove('svg')
      this.createViz()
    }
  }
}
</script>

<style>

</style>