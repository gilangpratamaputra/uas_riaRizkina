<template>
  <div>
    <Header></Header>
    <div class="card">
      <div class="card-header">
        <h1>DETAIL</h1>
      </div>
      <div class="card-body">
        <table>
          <thead>
            
          </thead>
          <tbody>
            <tr v-if="matakuliah">
              <td>MATAKULIAH:&ensp;{{ matakuliah.matakuliah }}</td>
            </tr>
            <tr v-if="matakuliah">
              <td>SKS:&ensp;{{ matakuliah.sks }}</td>
            </tr>
            <tr v-else>
              <td colspan="2">Matakuliah tidak ditemukan.</td>
            </tr>
          </tbody>
        </table>
      </div>
      <div class="card-footer">
        <button
          type="submit"
          class="text-white mt-4 bg-red-700 hover:bg-red-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
        >
          <NuxtLink to="/"> Kembali</NuxtLink>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      matakuliah: null
    };
  },
  mounted() {
    this.getDataMatakuliah();
  },
  methods: {
    async getDataMatakuliah() {
      const id = this.$route.params.id;
      try {
        const response = await axios.get(`https://64abc8e39edb4181202e87b6.mockapi.io/akademik/v1/matakuliah/${id}`);
        this.matakuliah = response.data;
      } catch (error) {
        console.error(error);
      }
    }
  }
}
</script>

<style>
.card {
  border-radius: 0.5rem;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  background-color: #fff;
  margin: 2rem auto;
  width: 400px;
  padding: 1rem;
}

.card-header {
  text-align: center;
  padding-bottom: 1rem;
  border-bottom: 1px solid #ccc;
}

.card-body {
  padding: 1rem 0;
}

.card-footer {
  text-align: center;
  padding-top: 1rem;
}
</style>
