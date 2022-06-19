<template>
  <v-container fluid class="fill-height d-flex flex-column" style="background: grey">
    <h1 class="mb-3">SVG Shapes</h1>

    <svg height="400" width="500" style="background: red">
      <line x1="0" y1="0" x2="470" y2="200" style="stroke: #268db2; stroke-width: 40px" />

      <rect x="200" y="100" width="200" height="200" style="fill: green"/>

      <circle cx="50" cy="50" r="25" style="fill: purple" />

      <text x="270" y="25" font-family="sans-serif" font-size="25" fill="white">
        SVG text primitive
      </text>

      <!-- <g> is used to group and reuse elements -->
      <g id="triangle">
        <polyline points="10 35, 30 10, 50, 35" syle="fill: orange" />
      </g>

      <!-- reuse the triangle above -->
      <use xlink:href="#triangle" x="100" y="300" />
    </svg>

  </v-container>
</template>

<script>
export default {

}
</script>

<style>

</style>