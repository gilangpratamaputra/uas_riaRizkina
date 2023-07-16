<template>
  <Header></Header>
  <div class="container mx-auto my-8">
    <div class="relative overflow-x-auto">
      <form @submit.prevent="addData" class="max-w-md mx-auto">
        <div class="mb-6">
          <label for="mk" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Mata Kuliah</label>
          <input
            type="text"
            id="mk"
            v-model="mata_kuliah"
            class="shadow-sm bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500 dark:shadow-sm-light"
            required
          />
        </div>
        <div class="mb-6">
          <label for="sks" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">SKS</label>
          <input
            type="number"
            id="sks"
            v-model="sks"
            class="shadow-sm bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500 dark:shadow-sm-light"
            required
          />
        </div>
        <div class="flex justify-between">
          <button
            type="submit"
            class="text-white bg-green-700 hover:bg-green-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
          >
            Tambah Data
          </button>
          <button
            type="button"
            class="text-white bg-red-700 hover:bg-red-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
          >
            <NuxtLink to="/"> Kembali</NuxtLink>
          </button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      mata_kuliah: '',
      sks: ''
    };
  },
  methods: {
    async addData() {
      try {
        const response = await axios.post('https://64abc8e39edb4181202e87b6.mockapi.io/akademik/v1/matakuliah', {
          mata_kuliah: this.mata_kuliah,
          sks: this.sks
        });
        console.log(response.data); // Output the response from the API if needed
        // Reset form
        this.mata_kuliah = '';
        this.sks = '';

        // Navigate back to akademik/index.vue
        this.$router.push('/');
      } catch (error) {
        console.error(error);
      }
    }
  }
};
</script>

<style>
</style>
