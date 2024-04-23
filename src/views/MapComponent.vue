<!-- eslint-disable no-unused-vars -->
<template>
    <div id="map" class="map-container"></div>
  </template>
  
  <script>
  import L from 'leaflet';
  import 'leaflet/dist/leaflet.css';
  
  export default {
    name: 'MapComponent',
    props: {
      elevators: {
        type: Array,
        required: true
      }
    },
    data() {
      return {
        map: null,
        tileLayer: null,
        layers: [],
      };
    },
    mounted() {
      this.initMap();
      this.initLayers();
    },
    methods: {
      initMap() {
        this.map = L.map('map').setView([0, 0], 1); // Set to your default location and zoom level
        this.tileLayer = L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
          maxZoom: 19,
          attribution: '© OpenStreetMap contributors'
        });
  
        this.tileLayer.addTo(this.map);
      },
      initLayers() {
        this.elevators.forEach(elevator => {
          const marker = L.marker([elevator.latitude, elevator.longitude]).addTo(this.map);
          marker.bindPopup(`<strong>${elevator.location}</strong><br>Status: ${elevator.status}`);
          this.layers.push(marker);
        });
      }
    },
    watch: {
      elevators: {
        // eslint-disable-next-line no-unused-vars
        handler(newVal) {
          this.layers.forEach(layer => this.map.removeLayer(layer));
          this.layers = [];
          this.initLayers();
        },
        deep: true
      }
    }
  };
  </script>
  
  <style>
  .map-container {
    height: 400px; /* Set map height */
  }
  </style>
  