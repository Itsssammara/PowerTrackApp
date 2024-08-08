<template>
    <div>
      <canvas ref="chart"></canvas>
    </div>
  </template>
  
  <script>
  import { Chart, LineElement, CategoryScale, LinearScale, Title, Tooltip, Legend, LineController } from 'chart.js';
  
  // Register all necessary components
  Chart.register(LineController, LineElement, CategoryScale, LinearScale, Title, Tooltip, Legend);
  
  export default {
    props: {
      chartData: {
        type: Object,
        required: true,
      },
      options: {
        type: Object,
        default() {
          return {
            responsive: true,
            maintainAspectRatio: false,
          };
        },
      },
    },
    mounted() {
      this.renderChart();
    },
    methods: {
      renderChart() {
        try {
          const ctx = this.$refs.chart.getContext('2d');
          if (!ctx) {
            console.error('Failed to get chart context');
            return;
          }
          
          new Chart(ctx, {
            type: 'line', // Chart type
            data: this.chartData,
            options: this.options,
          });
        } catch (error) {
          console.error('Error rendering chart:', error);
        }
      },
    },
  };
  </script>
  
  <style scoped>
  /* Add your styles here */
  </style>
  