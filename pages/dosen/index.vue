<template>
  <div>
    <Header></Header>
    <h1 class="text-2xl font-bold mb-4">Data Dosen</h1>
    <table class="min-w-full bg-white border border-gray-300">
      <thead>
        <tr>
          <th class="py-2 px-4 border-b">No</th>
          <th class="py-2 px-4 border-b">Nama Dosen</th>
          <th class="py-2 px-4 border-b">Gelar</th>
          <th class="py-2 px-4 border-b">Program Studi</th>
          <th class="py-2 px-4 border-b">Aksi</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(dosen, index) in dosens" :key="dosen.id">
          <td class="py-2 px-4 border-b">{{ index + 1 }}</td>
          <td class="py-2 px-4 border-b">{{ dosen.nama_dosen }}</td>
          <td class="py-2 px-4 border-b">{{ dosen.gelar }}</td>
          <td class="py-2 px-4 border-b">{{ dosen.prodi }}</td>
          <td class="px-6 py-4">
            <button
              class="focus:outline-none text-white bg-gray-400 hover:bg-gray-500 focus:ring-4 focus:ring-gray-300 font-medium rounded-lg text-sm px-5 py-2.5 mr-2 mb-2 dark:focus:ring-gray-900"
              @click="editDosen(dosen.id)"
            >
              Edit
            </button>
            <button
              type="button"
              class="focus:outline-none text-white bg-yellow-400 hover:bg-yellow-500 focus:ring-4 focus:ring-yellow-300 font-medium rounded-lg text-sm px-5 py-2.5 mr-2 mb-2 dark:focus:ring-yellow-900"
              @click="showDetail(dosen)"
            >
              Detail
            </button>
            <button
              class="focus:outline-none text-white bg-red-400 hover:bg-red-500 focus:ring-4 focus:ring-red-300 font-medium rounded-lg text-sm px-5 py-2.5 mr-2 mb-2 dark:focus:ring-red-900"
              @click="deleteDosen(nama_dosen.id)"
            >
              Delete
            </button>
          </td>
        </tr>
      </tbody>
    </table>

    <div v-if="showAlert" class="bg-green-500 text-white px-4 py-2 mt-4 rounded">
      Data berhasil dihapus!
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';

export default {
  setup() {
    const dosens = ref([]);
    const showAlert = ref(false);

    onMounted(async () => {
      try {
        const response = await fetch('https://64abc8e39edb4181202e87b6.mockapi.io/akademik/v1/matakuliah/1/dosen');
        const data = await response.json();
        dosens.value = data;
      } catch (error) {
        console.error(error);
      }
    });

    const deleteDosen = async (id) => {
      try {
        const response = await fetch(`https://64abc8e39edb4181202e87b6.mockapi.io/akademik/v1/matakuliah/1/dosen/${id}`, {
          method: 'DELETE',
        });

        if (response.ok) {
          dosens.value = dosens.value.filter((dosen) => dosen.id !== id);
          showAlert.value = true;
          setTimeout(() => {
            showAlert.value = false;
          }, 3000);
        } else {
          console.error('Failed to delete data.');
        }
      } catch (error) {
        console.error(error);
      }
    };

    const editDosen = (id) => {
      // Implementasi logika untuk mengedit dosen
      console.log(`Edit dosen dengan ID: ${id}`);
    };

    const showDetail = (dosen) => {
      // Implementasi logika untuk menampilkan detail dosen
      console.log('Detail dosen:', dosen);
    };

    return {
      dosens,
      showAlert,
      deleteDosen,
      editDosen,
      showDetail,
    };
  },
};
</script>

<style>
/* Your CSS styles */
</style>
