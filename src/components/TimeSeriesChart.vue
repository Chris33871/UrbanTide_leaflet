<template>
  <div>
    <canvas ref="chartCanvas">h</canvas>
  </div>
</template>

<script>
import Chart from 'chart.js';

export default {
  data() {
    return {
      chart: null,
    };
  },
  props: {
    data: Object, // Data for the chart
  },
  mounted() {
    this.createChart();
  },
  methods: {
    createChart() {
      if (this.chart) {
        this.chart.destroy(); // Destroy any existing chart to prevent duplication
      }
      const ctx = this.$refs.chartCanvas.getContext('2d');
      this.chart = new Chart(ctx, {
        type: 'line',
        data: this.data,
        options: {
          // Chart options (customize as needed)
        },
      });
    },
  },
};
</script>
