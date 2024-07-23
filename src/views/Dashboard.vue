<template>
  <div>
    <div class="topbar">
      <div class="toggle" @click="toggleSidebar">
        <ion-icon name="menu-outline"></ion-icon>
      </div>
      <div class="search">
        <label>
          <input type="text" placeholder="Search here">
          <ion-icon name="search-outline"></ion-icon>
        </label>
      </div>
      <div class="user">
        <img src="assets/imgs/customer01.jpg" alt="User">
      </div>
    </div>

    <div class="cardBox">
      <div class="card">
        <div>
          <div class="numbers">1,504</div>
          <div class="cardName">Alerts</div>
        </div>
        <div class="iconBx">
          <ion-icon name="eye-outline"></ion-icon>
        </div>
      </div>
      <div class="card">
        <div>
          <div class="numbers">80</div>
          <div class="cardName">Memberships</div>
        </div>
        <div class="iconBx">
          <ion-icon name="cart-outline"></ion-icon>
        </div>
      </div>
      <div class="card">
        <div>
          <div class="numbers">284</div>
          <div class="cardName">Due Bills</div>
        </div>
        <div class="iconBx">
          <ion-icon name="chatbubbles-outline"></ion-icon>
        </div>
      </div>
      <div class="card">
        <div>
          <div class="numbers">R$7,842</div>
          <div class="cardName">Current Balance</div>
        </div>
        <div class="iconBx">
          <ion-icon name="cash-outline"></ion-icon>
        </div>
      </div>
    </div>

    <div class="chart-container">
      <canvas id="financialChart"></canvas>
    </div>

    <div class="details">
      <div class="recentOrders">
        <div class="cardHeader">
          <h2>All Bills</h2>
          <a href="#" class="btn">View All</a>
        </div>
        <table>
          <thead>
            <tr>
              <td>Name</td>
              <td>Price</td>
              <td>Payment</td>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>Star Refrigerator</td>
              <td>$1200</td>
              <td>Paid</td>
            </tr>
            <tr>
              <td>Dell Laptop</td>
              <td>$110</td>
              <td>Due</td>
            </tr>
            <tr>
              <td>Apple Watch</td>
              <td>$1200</td>
              <td>Paid</td>
            </tr>
            <tr>
              <td>Addidas Shoes</td>
              <td>$620</td>
              <td>Due</td>
            </tr>
            <tr>
              <td>Star Refrigerator</td>
              <td>$1200</td>
              <td>Paid</td>
            </tr>
            <tr>
              <td>Dell Laptop</td>
              <td>$110</td>
              <td>Due</td>
            </tr>
            <tr>
              <td>Apple Watch</td>
              <td>$1200</td>
              <td>Paid</td>
            </tr>
            <tr>
              <td>Addidas Shoes</td>
              <td>$620</td>
              <td>Due</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
import { Chart, registerables } from 'chart.js';

Chart.register(...registerables);

export default {
  name: 'Dashboard',
  methods: {
    toggleSidebar() {
      const navigation = document.querySelector('.navigation');
      const main = document.querySelector('.main');
      navigation.classList.toggle('active');
      main.classList.toggle('active');
    },
    initializeChart() {
      var currencySymbol = 'R$';
      var ctx = document.getElementById('financialChart').getContext('2d');
      var financialChart = new Chart(ctx, {
        type: 'line',
        data: {
          labels: ['January', 'February', 'March', 'April', 'May', 'June'],
          datasets: [
            {
              label: 'Profits',
              data: [25.90, 700, 550, 800, 650, 900],
              borderColor: 'rgba(75, 192, 192, 1)',
              backgroundColor: 'rgba(75, 192, 192, 0.3)',
              fill: true,
              tension: 0.4
            },
            {
              label: 'Spending',
              data: [300, 400, 350, 500, 450, 600],
              borderColor: 'rgba(255, 99, 132, 1)',
              backgroundColor: 'rgba(255, 99, 132, 0.3)',
              fill: true,
              tension: 0.4
            }
          ]
        },
        options: {
          responsive: true,
          maintainAspectRatio: false,
          plugins: {
            tooltip: {
              mode: 'index',
              callbacks: {
                afterBody: function (tooltipItems) {
                  let profit = tooltipItems[0].parsed.y;
                  let spending = tooltipItems[1].parsed.y;
                  let balance = profit - spending;
                  let balanceFormatted = balance.toFixed(2);
                  let balanceDisplay = balance >= 0 ? `Positive (${currencySymbol}${balanceFormatted})` : `Negative (${currencySymbol}${Math.abs(balanceFormatted)})`;

                  return `Balance: ${balanceDisplay}`;
                }
              }
            }
          },
          scales: {
            y: {
              beginAtZero: true,
              ticks: {
                callback: function (value) {
                  return currencySymbol + value.toFixed(2);
                }
              }
            }
          }
        }
      });
    }
  },
  mounted() {
    this.initializeChart();
  }
};
</script>

<style scoped>
@import '../assets/css/style.css';
</style>
