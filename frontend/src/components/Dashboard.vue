<template>
    <div class="dashboard">
      <h1>Energy Data Dashboard</h1>
      <line-chart :chart-data="chartData" />
      <bar-chart :chart-data="chartData" />
    </div>
  </template>
  
  <script>
  import LineChart from './LineChart.vue';
  import BarChart from './BarChart.vue';
  
  export default {
    components: {
      LineChart,
      BarChart,
    },
    data() {
      return {
        chartData: {
          labels: ['January', 'February', 'March', 'April', 'May', 'June', 'July'],
          datasets: [
            {
              label: 'Energy Produced (kWh)',
              backgroundColor: '#42A5F5',
              data: [65, 59, 80, 81, 56, 55, 40],
            },
            {
              label: 'Energy Consumed (kWh)',
              backgroundColor: '#9ACDDA',
              data: [28, 48, 40, 19, 86, 27, 90],
            },
          ],
        },
      };
    },
  };
  </script>
  
  <style scoped>
  .dashboard {
    margin: 20px;
  }
  </style>  