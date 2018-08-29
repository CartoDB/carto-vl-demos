<template>
  <div id="map" ref="map"></div>
</template>

<script>
// TODO: change to `import carto from '@carto/carto-vl'` for next releases
import * as carto from '@carto/carto-vl'
import mapboxgl from '@carto/mapbox-gl'
import '@carto/mapbox-gl/dist/mapbox-gl.css'

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
    const map = this.createMap();
    const layer = this.createLayer();

    layer.addTo(map, 'watername_ocean')
  },
  methods: {
    createMap: function () {
      return new mapboxgl.Map({
        container: 'map',
        style: basemaps[this.basemap],
        center: [0, 30],
        zoom: 2
      })
    },
    createLayer: function () {
      const source = new carto.source.Dataset(datasets[this.geom], {
        user: 'cartovl',
        apiKey: 'default_public'
      })
      const viz = new carto.Viz()
      return new carto.Layer('layer', source, viz)
    }
  }
}
</script>

<style scoped>
#map {
  height: 100%;
  width: 100%;
}
</style>
