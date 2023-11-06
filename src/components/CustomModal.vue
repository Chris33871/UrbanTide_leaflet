<template>
    <div v-if="showModal" class="custom-modal">
      <div class="modal-content">
        <button @click="closeModal" class="close-button">Close</button>
        <div class="modal-body">
          <!-- Your chart component goes here -->
          <TimeSeriesChart :data="chartData" ref="chart" />
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import TimeSeriesChart from './TimeSeriesChart.vue'; // Import your TimeSeriesChart component
  
  export default {
    props: {
      showModal: Boolean,
      chartData: Object,
    },
    components: {
      TimeSeriesChart,
    },
    methods: {
      closeModal() {
        this.$emit('close'); // Emit a custom event to close the modal
      },
    },
  };
  </script>
  
  <style scoped>
  /* Style your custom modal here */
  .custom-modal {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 999;
  }
  
  .modal-content {
    background-color: #fff;
    padding: 20px;
    border-radius: 5px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
    max-width: 80%;
    max-height: 80%;
    overflow: auto;
    position: relative;
  }
  
  .close-button {
    position: absolute;
    top: 10px;
    right: 10px;
    cursor: pointer;
  }
  
  .modal-body {
    /* Customize modal body styles */
  }
  </style>
  