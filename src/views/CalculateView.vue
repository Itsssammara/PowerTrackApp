
<template>
  <div class="data text-light">
    <h1>Solar Irradiance Estimation</h1>
    <div>
      <input v-model="location" placeholder="Enter location (e.g., city name)">
      <button @click="fetchWeatherData">Search</button>
    </div>
    <!-- Input fields for solar array surface area, panel efficiency, and daily consumption -->
    <div class="form-group">
      <label for="panelArea">Solar Array Surface Area (m²)</label>
      <input type="number" id="panelArea" v-model="panelArea" placeholder="e.g., 10" min="0">
    </div>
    <div class="form-group">
      <label for="efficiency">Panel Efficiency</label>
      <select id="efficiency" v-model="efficiency">
        <option value="15">Standard (15%)</option>
        <option value="18">High Efficiency (18%)</option>
        <option value="20">Premium (20%)</option>
      </select>
    </div>
    <div class="form-group">
      <label for="dailyConsumption">Daily Consumption (kWh)</label>
      <input type="number" id="dailyConsumption" v-model="dailyConsumption" placeholder="e.g., 5" min="0">
    </div>
    <!-- Display weather data and calculated power output -->
    <div v-if="weatherData.length">
      <table>
        <thead>
          <tr>
            <th>Date & Time</th>
            <th>Cloud Cover (%)</th>
            <th>Estimated Solar Irradiance (W/m²)</th>
            <th>Temperature (°C)</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(weather, index) in weatherData" :key="index">
            <td>{{ formatDateTime(weather.dateTime) }}</td>
            <td>{{ weather.clouds }}</td>
            <td>{{ estimateIrradiance(weather.clouds) }}</td>
            <td>{{ weather.temp }}</td>
          </tr>
        </tbody>
      </table>
      <div v-if="totalPowerOutput !== null">
        <h2>Total Power Output: {{ totalPowerOutput }} kWh</h2>
        <h2>Net Power After Consumption: {{ netPowerOutput }} kWh</h2>
      </div>
    </div>
    <div v-else>
      <p>No data available. Please enter a valid location.</p>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      location: '', // User input for location
      weatherData: [], // Weather data fetched from the API
      apiKey: 'e945d7f71eb0e5e621a7dfcce2cb1a43', // Replace with your actual API key
      panelArea: 10, // Default solar array surface area
      efficiency: 15, // Default panel efficiency
      dailyConsumption: 5, // Default daily consumption
      totalPowerOutput: null, // Total power output calculation
      netPowerOutput: null, // Net power output after consumption
    };
  },
  methods: {
    estimateIrradiance(cloudCover) {
      const clearSkyIrradiance = 1000; // Example clear-sky value in W/m²
      return clearSkyIrradiance * (1 - cloudCover / 100);
    },
    formatDateTime(timestamp) {
      const date = new Date(timestamp * 1000);
      const formattedDate = date.toLocaleDateString();
      const formattedTime = date.toLocaleTimeString();
      return `${formattedDate} ${formattedTime}`;
    },
    async fetchWeatherData() {
      if (!this.location) {
        alert('Please enter a location.');
        return;
      }
      const url = `https://api.openweathermap.org/data/2.5/forecast?q=${this.location}&appid=${this.apiKey}&units=metric`;
      try {
        const response = await fetch(url);
        const data = await response.json();
        if (data.cod !== "200") {
          alert('Location not found.');
          this.weatherData = [];
          this.totalPowerOutput = null;
          this.netPowerOutput = null;
          return;
        }
        // Filter data for the current date
        const today = new Date().toISOString().split('T')[0];
        this.weatherData = data.list
          .filter(item => {
            const itemDate = new Date(item.dt * 1000).toISOString().split('T')[0];
            return itemDate === today;
          })
          .map(item => ({
            dateTime: item.dt,
            clouds: item.clouds.all,
            temp: item.main.temp,
          }));
        // Calculate the total power output and net power output based on the filtered weather data
        this.calculatePowerOutputs();
      } catch (error) {
        console.error('Error fetching weather data:', error);
        alert('An error occurred while fetching the weather data.');
      }
    },
    calculatePowerOutputs() {
      if (this.weatherData.length === 0 || !this.panelArea || !this.efficiency) {
        this.totalPowerOutput = null;
        this.netPowerOutput = null;
        return;
      }
      const totalIrradiance = this.weatherData.reduce((sum, weather) => {
        return sum + this.estimateIrradiance(weather.clouds);
      }, 0);
      const panelAreaInM2 = parseFloat(this.panelArea);
      const efficiencyInDecimal = parseFloat(this.efficiency) / 100;
      // Convert W/m² to kW (divide by 1000) and multiply by the number of hours in the forecast period
      const hoursInForecast = this.weatherData.length * 3; // assuming 3-hour intervals
      this.totalPowerOutput = (totalIrradiance * panelAreaInM2 * efficiencyInDecimal * hoursInForecast) / 1000; // kWh
      // Calculate the net power output after daily consumption
      const dailyConsumptionInKWh = parseFloat(this.dailyConsumption);
      this.netPowerOutput = this.totalPowerOutput - dailyConsumptionInKWh;
    },
  },
};
</script>
<style>
body {
  padding-bottom: 10%;
  margin: 0;
  font-family: 'Arial', sans-serif;
  background-size: cover;
  background-position: center;
  background-attachment: fixed;
}

.data {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  color: #fff;
  background: rgba(0, 0, 0, 0.6);
  border-radius: 10px;
  box-shadow: 0 0 15px rgba(0, 0, 0, 0.5);
  backdrop-filter: blur(10px);
}

h1 {
  text-align: center;
  margin-bottom: 20px;
  font-size: 1.8em;
}

.form-group {
  margin-bottom: 15px;
}

label {
  display: block;
  margin-bottom: 5px;
  font-weight: bold;
}

input,
select {
  width: calc(100% - 16px);
  padding: 10px;
  margin: 8px 0;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 1em;
  background-color: rgba(255, 255, 255, 0.9);
  box-shadow: inset 0 1px 2px rgba(0, 0, 0, 0.1);
}

input::placeholder {
  color: #999;
}

button {
  width: 100%;
  padding: 10px;
  background-color: #28a745;
  color: #fff;
  border: none;
  border-radius: 5px;
  font-size: 1em;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #218838;
}

table {
  width: 100%;
  margin-top: 20px;
  border-collapse: collapse;
  background: rgba(255, 255, 255, 0.9);
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
}

th,
td {
  padding: 12px;
  text-align: left;
  border-bottom: 1px solid #ddd;
  font-size: 0.9em;
}

th {
  background-color: #333;
  color: #fff;
}

tr:nth-child(even) {
  background-color: #f2f2f2;
}

tr:hover {
  background-color: #ddd;
}

h2 {
  text-align: center;
  margin-top: 20px;
  font-size: 1.5em;
}

p {
  text-align: center;
  font-size: 1.1em;
  color: #ff4c4c;
}

</style>