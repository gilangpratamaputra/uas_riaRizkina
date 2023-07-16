<template>
  <Header></Header>
  <div v-if="showAlert" class="bg-green-500 text-white px-4 py-2 mt-4 rounded">
        Data berhasil dihapus!
      </div>
  <div class="container mx-auto my-8">
    <div class="relative overflow-x-auto">
      <button class="focus:outline-none text-white bg-gray-400 hover:bg-gray-500 focus:ring-4 focus:ring-gray-300 font-medium rounded-lg text-sm px-5 py-2.5 mr-2 mb-2 dark:focus:ring-gray-900" @click="$router.push('/matakuliah/CreateData')">Tambah Data</button>
      <table class="w-full">
        <thead>
          <tr>
            <th class="px-6 py-3">No</th>
            <th class="px-6 py-3">Mata Kuliah</th>
            <th class="px-6 py-3">SKS</th>
            <th class="px-6 py-3">Action</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="mk in matakuliah" :key="mk.id" class="bg-white dark:bg-gray-800">
            <td class="px-6 py-4">{{ mk.id }}</td>
            <td class="px-6 py-4">{{ mk.matakuliah }}</td>
            <td class="px-6 py-4">{{ mk.sks }}</td>
            <td class="px-6 py-4">
              <button class="focus:outline-none text-white bg-gray-400 hover:bg-gray-500 focus:ring-4 focus:ring-gray-300 font-medium rounded-lg text-sm px-5 py-2.5 mr-2 mb-2 dark:focus:ring-gray-900" @click="editMatakuliah(mk.id)">Edit</button>
              <button type="button" class="focus:outline-none text-white bg-yellow-400 hover:bg-yellow-500 focus:ring-4 focus:ring-yellow-300 font-medium rounded-lg text-sm px-5 py-2.5 mr-2 mb-2 dark:focus:ring-yellow-900">
                <NuxtLink :to="`/matakuliah/${mk.id}`">Detail</NuxtLink>
              </button>
              <button class="focus:outline-none text-white bg-red-400 hover:bg-red-500 focus:ring-4 focus:ring-red-300 font-medium rounded-lg text-sm px-5 py-2.5 mr-2 mb-2 dark:focus:ring-red-900" @click="deleteMatakuliah(mk.id)">Delete</button>
            </td>
          </tr>
        </tbody>
      </table>
      
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      matakuliah: [],
      showAlert: false
    };
  },
  mounted() {
    this.getDataMatakuliah();
  },
  methods: {
    async getDataMatakuliah() {
      try {
        const response = await axios.get('https://64abc8e39edb4181202e87b6.mockapi.io/akademik/v1/matakuliah');
        this.matakuliah = response.data;
      } catch (error) {
        console.error(error);
      }
    },
    async deleteMatakuliah(id) {
      try {
        await axios.delete(`https://64abc8e39edb4181202e87b6.mockapi.io/akademik/v1/matakuliah/${id}`);
        this.matakuliah = this.matakuliah.filter(mk => mk.id !== id);
        this.showAlert = true; // Menampilkan pesan alert
        setTimeout(() => {
          this.showAlert = false; // Menghilangkan pesan alert setelah beberapa detik
        }, 9000);
      } catch (error) {
        console.error(error);
      }
    },
    editMatakuliah(id) {
      // Implementasi logika untuk mengedit matakuliah
      console.log(`Edit matakuliah dengan ID: ${id}`);
    }
  }
};
</script>

<style scoped>
table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 20px;
}

th, td {
  padding: 8px;
  border-bottom: 1px solid #ddd;
}

th {
  background-color: #f2f2f2;
  font-weight: bold;
  text-align: left;
}

button {
  padding: 6px 10px;
  margin-right: 4px;
  border: none;
  cursor: pointer;
}

/* Style for alert message */
.alert {
  background-color: #48bb78;
}

.alert p {
  color: #fff;
  margin: 0;
  padding: 0.5rem;
}
</style>
