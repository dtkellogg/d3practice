<template>
  <div>
    <h1 style="text-align: center">Data Basics</h1>

    <h2 class="mt-7" style="text-align: center">Using Existing DOM Elements</h2>
    <table style="width: 100%">
      <thead>
        <tr class="head">
          <th scope="col" class="head-date">Date</th>
          <th scope="col" class="head-temp-low">Low</th>
          <th scope="col" class="head-temp-high">High</th>
        </tr>
      </thead>
      <tbody>
        <tr class="day">
          <th class="day-date">06/18/22</th>
          <td class="day-low"><span class="temp">57</span>&deg;</td>
          <td class="day-high"><span class="temp">87</span>&deg;</td>
        </tr>
        <tr class="day">
          <th class="day-date">06/19/22</th>
          <td class="day-low"><span class="temp">44</span>&deg;</td>
          <td class="day-high"><span class="temp">83</span>&deg;</td>
        </tr>
        <tr class="day">
          <th class="day-date">06/20/22</th>
          <td class="day-low"><span class="temp">52</span>&deg;</td>
          <td class="day-high"><span class="temp">91</span>&deg;</td>
        </tr>
        <tr class="day">
          <th class="day-date">06/21/22</th>
          <td class="day-low"><span class="temp">48</span>&deg;</td>
          <td class="day-high"><span class="temp">99</span>&deg;</td>
        </tr>
        <tr class="day">
          <th class="day-date">06/22/22</th>
          <td class="day-low"><span class="temp">50</span>&deg;</td>
          <td class="day-high"><span class="temp">102</span>&deg;</td>
        </tr>
      </tbody>
    </table>

    <h2 class="mt-7" style="text-align: center">Inserting Data into New DOM Elements</h2>
    <table style="width: 100%" class="table-2">
      <thead>
        <tr class="head">
          <th scope="col" class="head-date">Date</th>
          <th scope="col" class="head-temp-low">Low</th>
          <th scope="col" class="head-temp-high">High</th>
        </tr>
      </thead>
      <tbody class="tbody-2">
      </tbody>
    </table>

  </div>
</template>

<script>
import * as d3 from 'd3'
export default {
  data() {
    return {
      dates: [
        {date: '06/18/22', low: 55, high: 83},
        {date: '06/19/22', low: 45, high: 77},
        {date: '06/20/22', low: 57, high: 89},
        {date: '06/21/22', low: 59, high: 94},
        {date: '06/22/22', low: 51, high: 93}
      ]
    }
  },
  mounted() {
    d3.selectAll('.day-high .temp')
      .data([666, 777, 888, 999])  // if the data arr only has 4 elements, only 4 elements will be replaced
      .html((d) => {
        // return d
        return '<em>' + d + '</em>'
      })

    d3.selectAll('.day-low .temp')
      .data([10, 20, 30])
      .html((d,i) => {
        if(i === 0) return '<b class="yellow--text">' + d + '</b>'
        else {
          if (d <= 20) return '<b class="blue--text">' + d + '</b>'
          return '<b>' + d + '</b>'
        }
      })

    d3.select('.tbody-2')
      .selectAll('tr')  // Select tr's that you haven't created yet
      .data(this.dates)
      .enter().append('tr')  // Creating the bars after you select them
      .html((d) => {
        return '<th scope="row">' + d.date + '</th>' +
                '<td style="text-align: center">' + d.low + '</td>' +
                '<td style="text-align: center">' + d.high + '</td>'
      })
  }
}
</script>

<style>
  .day-low, .day-high {
    text-align: center;
  }

  h2 {
    padding-bottom: 30px !important;
  }
</style>