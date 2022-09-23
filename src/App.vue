<template>
  <div id="app">
    <header>
      <h1>Vue.js SPA</h1>
    </header>
    <main>
      <aside class="sidebar">
        <div v-for="employee in employees" v-bind:key="employee.id">
          {{ employee.surname }} {{ employee.name }} {{ employee.patronymic }}
        </div>
      </aside>
      <div class="content">
      </div>
    </main>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data () {
    return {
      employees: null,
      endpoint: 'http://localhost:8080/equipment/user/all'
    }
  },
  created() {
    this.getAllEmployees();
  },
  methods: {
    getAllEmployees() {
      let config = {
        headers: {
          "Content-Type": "application/json",
          "Access-Control-Allow-Origin": "*",
          "Access-Control-Allow-Methods": "POST,GET,OPTIONS, PUT, DELETE",
          "Access-Control-Allow-Headers": "Accept, Content-Type, Content-Length, Accept-Encoding, X-CSRF-Token, Authorization"
        },
        auth: {
          username: 'user',
          password: '123'
        }
      }

      axios.get(this.endpoint, config)
          .then(response => {
            this.employees = response.data;
          })
          .catch(error => {
            console.log("-------error-------");
            console.log(error);
          })
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
