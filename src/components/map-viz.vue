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
      :lat-lng="marker.coordinates"
      @mouseover="openPopup"
      @mouseout="closePopup">
      <l-popup ref="popup">
        {{ marker.count }}
      </l-popup>
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

// Fix for broken marker icons
import L from 'leaflet';
delete L.Icon.Default.prototype._getIconUrl;

L.Icon.Default.mergeOptions({
  iconRetinaUrl: require('leaflet/dist/images/marker-icon-2x.png'),
  iconUrl: require('leaflet/dist/images/marker-icon.png'),
  shadowUrl: require('leaflet/dist/images/marker-shadow.png'),
});

export default {
  components: {
    LMap,
    LTileLayer,
    LMarker
  },
  data () {
    return {
      url: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
      center: [55.8642, -3.7079],
      zoom: 10,
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
    },
    openPopup() {
      this.$refs.popup.openPopup();
    },
    closePopup() {
      this.$refs.popup.closePopup();
    }
  },
  created() {
    fetch('https://api.usmart.io/org/d1b773fa-d2bd-4830-b399-ecfd18e832f3/657f6f93-932b-4851-ae21-830b321c185d/latest/urql')
      .then(response => response.json())
      .then(data => {
        this.markers = data.map(item => ({
          id: item.usmart_id,
          coordinates: [item.latitude, item.longitude],
          count: item.count
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