<template>
    <div class="modal" v-if="showModal">
      <div class="modal-content">
        <!-- Display time series data here -->
        <button @click="showModal = false">Close</button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        showModal: false,
      };
    },
    methods: {
      openModal() {
        this.showModal = true;
      },
    },
  };
  </script>