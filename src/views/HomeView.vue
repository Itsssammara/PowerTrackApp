<template>
  <div id="app">
    <div class="container">
      <h1>Energy Calculator</h1>
      <div class="form-group">
        <label for="day">Select Day:</label>
        <input type="number" id="day" v-model="day">
      </div>
      <div class="form-group">
        <label for="capacity">Energy Generated (kWh):</label>
        <input type="number" id="capacity" v-model.number="capacity" step="0.01" placeholder="Enter energy generated">
      </div>
      <div class="form-group">
        <label for="energyUsed">Energy Used (kWh):</label>
        <input type="number" id="energyUsed" v-model.number="energyUsed" step="0.01" placeholder="Enter energy used">
      </div>
      <div class="button-group">
        <button @click="calculateReturn">Calculate</button>
        <button @click="fetchData">Fetch Data</button>
      </div>
      <div class="result">{{ resultMessage }}</div>
      <canvas id="energyChart" width="400" height="200"></canvas>
    </div>

    <div id="register">
      <div id="ticket">
        <h1>Your Receipt</h1>
        <table>
          <tbody id="entries">
            <tr>
              <td>Units Sent Back</td>
              <td>{{ savedUnits.toFixed(2) }} kWh</td>
            </tr>
          </tbody>
          <tfoot>
            <tr>
              <th>Amount Paid Back:</th>
              <th id="total">R {{ totalMoneyEarned.toFixed(2).replace('.', ',') }}</th>
            </tr>
          </tfoot>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
import { mapActions, mapState } from 'vuex';

export default {
  data() {
    return {
      day: null
    };
  },
  computed: {
    ...mapState(['capacity', 'energyUsed', 'totalMoneyEarned']),
    savedUnits() {
      return this.capacity - this.energyUsed;
    },
    resultMessage() {
      if (this.capacity && this.energyUsed !== null) {
        return `Energy Generated - ${this.capacity} kWh, Energy Used - ${this.energyUsed} kWh`;
      }
      return '';
    }
  },
  methods: {
    ...mapActions(['fetchData', 'calculateReturn']),
    async fetchData() {
      if (!this.day) {
        this.resultMessage = 'Please select a day.';
        return;
      }

      await this.$store.dispatch('fetchData', this.day);

      this.resultMessage = `Data fetched: Energy Generated: ${this.capacity} kWh, Energy Used: ${this.energyUsed} kWh`;

      this.calculateReturn();
      this.updateChart();
    },
    calculateReturn() {
      this.$store.dispatch('calculateReturn');
    },
    updateChart() {
      const ctx = document.getElementById('energyChart').getContext('2d');
      if (this.chart) {
        this.chart.destroy();
      }
      this.chart = new Chart(ctx, {
        type: 'bar',
        data: {
          labels: ['Energy Generated', 'Energy Used', 'Excess Energy'],
          datasets: [{
            label: 'Energy (kWh)',
            data: [this.capacity, this.energyUsed, this.savedUnits],
            backgroundColor: ['#ff9a00', '#ffcc00', '#66cc66'],
            borderColor: ['#e87c00', '#ffd700', '#44aa44'],
            borderWidth: 1
          }]
        },
        options: {
          responsive: true,
          scales: {
            x: {
              beginAtZero: true
            },
            y: {
              beginAtZero: true
            }
          }
        }
      });
    }
  },
  watch: {
    capacity() {
      this.updateChart();
    },
    energyUsed() {
      this.updateChart();
    }
  }
};
</script>

<style>
body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background: linear-gradient(to right, #9ACDDA, #D90700); /* Updated gradient */
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    width: 100%;
    margin: 0;
}

#app {
    width: 100%;
    max-width: 800px;
    display: flex;
    flex-direction: row;
    align-items: center;
}

.container {
    background: #ffffff; /* Light background for the calculator */
    padding: 20px;
    border-radius: 12px;
    box-shadow: 0 4px 8px rgba(0,0,0,0.2);
    max-width: 500px;
    width: 100%;
    margin: 20px;
    height: auto;
}

h1 {
    color: #333;
    margin-bottom: 20px;
    font-size: 22px;
    font-weight: 600;
    background: linear-gradient(90deg, #9ACDDA, #D90700); /* Gradient for heading */
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
}

.form-group {
    margin-bottom: 15px;
}

.form-group label {
    display: block;
    margin-bottom: 6px;
    font-weight: 500;
    color: #555;
}

.form-group input {
    width: 100%;
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 8px;
    box-sizing: border-box;
    font-size: 14px;
}

.form-group input:focus {
    border-color: #D90700; /* Red for focus border */
    outline: none;
    box-shadow: 0 0 5px rgba(217, 7, 0, 0.5);
}

.button-group {
    display: flex;
    justify-content: center;
    gap: 8px;
}

button {
    background-color: #D90700; /* Red for buttons */
    color: white;
    border: none;
    padding: 10px 16px;
    border-radius: 8px;
    font-size: 16px;
    cursor: pointer;
    transition: background-color 0.3s ease;
}

button:hover {
    background-color: #a80000; /* Darker shade of red for hover */
}

.result {
    margin-top: 15px;
    font-size: 16px;
    font-weight: 600;
    color: #28a745; /* Green for success messages */
    text-align: center;
}

#error {
    color: #D90700; /* Red for errors */
    font-size: 16px;
    font-weight: 500;
}

.success {
    color: #2ecc71; /* Green for success messages */
    font-size: 16px;
    font-weight: 500;
}

#register {
    width: 100%;
    max-width: 500px;
}

#ticket {
    background: #ffffff; /* White background for the ticket */
    margin: auto;
    padding: 1em;
    border-radius: 12px;
    box-shadow: 0 0 5px rgba(0,0,0,.25);
}

#ticket h1 {
    text-align: center;
    color: #D90700; /* Red for heading */
}

#ticket table {
    font-family: 'Courier New', Courier, monospace;
    width: 100%;
    border-collapse: collapse;
}

#ticket td, #ticket th {
    padding: 8px;
}

#ticket th {
    text-align: left;
    background-color: #f7f7f7;
}

#ticket td, #ticket #total {
    text-align: left;
}

#ticket tfoot th {
    border-top: 1px solid #ddd;
    font-size: 14px;
    background-color: #f7f7f7;
}

</style>
