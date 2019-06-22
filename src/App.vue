<template>
  <div id="app">
    <b-navbar variant="faded" type="light">
      <b-navbar-brand href="/">
        <i class="fab fa-bitcoin"></i> Bitcurrency
      </b-navbar-brand>
    </b-navbar>
    <div class="container">
      <section class="chart-container">
        <h2>Últimas ordens</h2>
        <highcharts :options="chartOptions"></highcharts>
      </section>
      <section class="table-container">
        <div class="table-responsive">
          <table class="table table-striped">
            <thead>
              <th>Tipo</th>
              <th>Quantidade (BTC)</th>
              <th>Preço unitário (R$)</th>
              <th>Total em reais</th>
            </thead>
            <tbody>
              <tr v-for="order in orders" :key="order.index">
                <td>{{ order.type }}</td>
                <td>{{ order.amount }}</td>
                <td>{{ order.unit_price }}</td>
                <td>{{ formatPrice(order.unit_price * order.amount) }}</td>
              </tr>
            </tbody>
          </table>
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import { Chart } from "highcharts-vue";
import BootstrapVue from "bootstrap-vue";

Vue.use(BootstrapVue);

import "bootstrap/dist/css/bootstrap.css";
import "bootstrap-vue/dist/bootstrap-vue.css";
import "@fortawesome/fontawesome-free/css/all.min.css";

import Vue from "vue";

export default {
  name: "app",
  components: {
    highcharts: Chart
  },
  data() {
    return {
      orders: [
        { amount: 0.00218914, unit_price: 40580, type: "Compra" },
        { amount: 0.00294201, unit_price: 40400, type: "Venda" },
        { amount: 0.00149585, unit_price: 40510, type: "Compra" },
        { amount: 1.05171087, unit_price: 40450, type: "Compra" },
        { amount: 2.00149585, unit_price: 40550, type: "Compra" },
        { amount: 0.02148535, unit_price: 40600, type: "Venda" },
        { amount: 0.01235345, unit_price: 40700, type: "Venda" },
        { amount: 1.91238123, unit_price: 40450, type: "Compra" },
        { amount: 2.12367675, unit_price: 40600, type: "Venda" },
        { amount: 0.00345955, unit_price: 40650, type: "Compra" }
      ],
      price_list: [],
      chartOptions: {
        series: [
          {
            data: [
              40580,
              40400,
              40510,
              40450,
              40550,
              40600,
              40700,
              40450,
              40600,
              40650
            ]
          }
        ],
        title: {
          text: ""
        },
        yAxis: {
          title: {
            text: "Preço (R$)"
          }
        },
        xAxis: {
          categories: [
            "Compra",
            "Venda",
            "Compra",
            "Compra",
            "Compra",
            "Venda",
            "Venda",
            "Compra",
            "Venda",
            "Compra"
          ]
        }
      }
    };
  },
  methods: {
    formatPrice(value) {
      let val = (value / 1).toFixed(2).replace(".", ",");
      return val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".");
    }
  }
};
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  .navbar {
    background: linear-gradient(to bottom, #000428, #002b75);
    box-shadow: 0 0 5px black;
    margin-bottom: 2rem;
    a {
      color: white;
    }
  }
  .table-container {
    margin-top: 5rem;
  }
  .table-striped tbody tr:nth-of-type(odd) {
    background-color: rgba(45, 45, 45, 0.51);
  }
}
</style>
