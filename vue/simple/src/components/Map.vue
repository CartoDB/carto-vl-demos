<template>
  <div id="map" ref="map"></div>
</template>

<script>
const carto = require('@carto/carto-vl')
// import carto from '@carto/carto-vl'
import mapboxgl from '@carto/mapbox-gl'

export default {
  name: 'Map',
  props: {
    basemap: {
      default: 'voyager',
      type: String
    },
    geom: {
      default: 'points',
      type: String
    }
  },
  mounted: function () {
    const basemaps = {
      'voyager': 'https://basemaps.cartocdn.com/gl/voyager-gl-style/style.json',
      'positron': 'https://basemaps.cartocdn.com/gl/positron-gl-style/style.json',
      'dark-matter': 'https://basemaps.cartocdn.com/gl/dark-matter-gl-style/style.json'
    }

    const datasets = {
      'points': 'ne_10m_populated_places_simple',
      'lines': 'ne_50m_rivers_lake_centerlines',
      'polygons': 'world_borders'
    }

    const map = new mapboxgl.Map({
      container: 'map',
      style: basemaps[this.basemap],
      center: [0, 30],
      zoom: 2
    })

    const source = new carto.source.Dataset(datasets[this.geom], {
      user: 'cartovl',
      apiKey: 'default_public'
    })
    const viz = new carto.Viz()
    const layer = new carto.Layer('layer', source, viz)

    layer.addTo(map, 'watername_ocean')
  }
}
</script>

<style scoped>
#map {
  height: 100%;
  width: 100%;
}
</style>
