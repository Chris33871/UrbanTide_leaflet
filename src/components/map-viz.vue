<template>
  <l-map
    :center="center"
    :zoom="zoom"
    class="map"
    ref="map"
    @update:zoom="zoomUpdated"
    @update:center="centerUpdated"
  >
    <l-marker 
      v-for="marker in markers"
      :key="marker.id"
      :lat-lng="marker.coordinates">
    </l-marker>
    <l-tile-layer
      :url="url"
    >
    </l-tile-layer>
  </l-map>
</template>

<script>
import { LMap, LTileLayer, LMarker } from 'vue2-leaflet';
import 'leaflet/dist/leaflet.css';

export default {
  components: {
    LMap,
    LTileLayer,
    LMarker
  },
  data () {
    return {
      url: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
      center: [ 49.1193089, 6.1757156 ],
      zoom: 12,
      markers: []
    }
  },
  methods: {
    zoomUpdated (zoom) {
      this.zoom = zoom;
      console.log(this.markers)
    },
    centerUpdated (center) {
      this.center = center;
    }
  },
  created() {
    fetch('https://api.usmart.io/org/d1b773fa-d2bd-4830-b399-ecfd18e832f3/657f6f93-932b-4851-ae21-830b321c185d/latest/urql')
      .then(response => response.json())
      .then(data => {
        this.markers = data.map(item => ({
          id: item.usmart_id,
          coordinates: [item.latitude, item.longitude]
        }));
      });
  }
}
</script>

<style>
  .map {
    position: absolute;
    width: 100%;
    height: 100%;
    overflow :hidden
  }
</style>