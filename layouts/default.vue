<template>
  <v-app dark>
    <v-navigation-drawer
      v-model="drawer"
      :mini-variant="miniVariant"
      :clipped="clipped"
      fixed
      app
    >
      <v-list>
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
        >
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="item.title" />
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar :clipped-left="clipped" fixed app>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-btn icon @click.stop="miniVariant = !miniVariant">
        <v-icon>mdi-{{ `chevron-${miniVariant ? 'right' : 'left'}` }}</v-icon>
      </v-btn>
      <v-btn icon @click.stop="clipped = !clipped">
        <v-icon>mdi-application</v-icon>
      </v-btn>
      <v-btn icon @click.stop="fixed = !fixed">
        <v-icon>mdi-minus</v-icon>
      </v-btn>
      <v-toolbar-title v-text="title" />
      <v-spacer />
      
    </v-app-bar>
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
    
    <v-footer :absolute="!fixed" app>
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  name: 'DefaultLayout',
  data() {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: 'mdi-apps',
          title: 'Home',
          to: '/',
        },
        {
          icon: 'mdi-format-color-text',
          title: 'Selections and Modifications',
          to: '/selectionsAndModifications',
        },
        {
          icon: 'mdi-shape',
          title: 'SVG Shapes',
          to: '/SVGShapes',
        },
        {
          icon: 'mdi-shape',
          title: 'SVG with D3',
          to: '/SVGWithD3',
        },
        {
          icon: 'mdi-database',
          title: 'Data',
          to: '/data',
        },
        {
          icon: 'mdi-chart-bar-stacked',
          title: 'Bar Graphs',
          to: '/bargraphs',
        },
        {
          icon: 'mdi-chart-bar',
          title: 'Bar Graph with Dynamic Data',
          to: '/bargraphdynamicdata',
        },
        {
          icon: 'mdi-chart-bar',
          title: 'Bar Graph Axes',
          to: '/bargraphaxes',
        },
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Damian\'s D3 Practice',
    }
  },
}
</script>
