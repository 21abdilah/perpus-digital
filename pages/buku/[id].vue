<template>
  <div class="container">
    <div v-if="loading">Loading data...</div>
    <h2 class="text-start my-4">{{ buku.judul }}</h2>
    <div class="row mt-5" v-if="!loading">
      <div class="col-md-3 ">
        <img :src="buku.cover" class="cover" alt="cover buku"/>
      </div>
      <div class=" col-md-9 p-5">
        <ul class="list-group list-group-flush">
          <li class="list-group-item">Judul: {{ buku.judul }}</li>
          <li class="list-group-item">Penulis: {{ buku.penulis }}</li>
          <li class="list-group-item">Penerbit: {{ buku.penerbit }}</li>
          <li class="list-group-item">Tahun Terbit: {{ buku.tahun_terbit }}</li>
          <li class="list-group-item">Rak: {{ buku.rak }}</li>
          <li class="list-group-item">
            <span v-if="buku.kategori">
              Kategori : {{ buku.kategori.nama }}
            </span>
            <span v-else> </span>
          </li>
          <li class="list-group-item">Deskripsi: {{ buku.deskripsi }}</li>
        </ul>
      </div>
    </div>
  </div>
  <div class="form-kembali">
    <nuxt-link to="../"
      ><button class="btn btn-light btn-lg rounded-4 px-4">
        KEMBALI
      </button></nuxt-link
    >
  </div>
</template>

<style scoped>
.form-kembali {
  position: fixed;
  bottom: 10px;
  left: 50%;
  transform: translateX(-50%);
}
.btn-dark {
  box-shadow: 1px 1px 10px #e4ecea !important;
}
.btn-light {
  background-color: #5fd8fe !important;
  box-shadow: 1px 1px 10px #5fd8fe !important;
}


.cover {
  width: 255px;
  height: 370px;
  box-shadow: 1px 10px 10px rgb(0, 0, 0, .5);
}

</style>

<script setup>
import { ref, onMounted } from 'vue';
const supabase = useSupabaseClient();

const route = useRoute();
const buku = ref({});
const loading = ref(true);

const getBookById = async () => {
  try {
    const { data, error } = await supabase
      .from("buku")
      .select(`*, kategori(*)`)
      .eq("id", route.params.id);
    if (data && data.length > 0) {
      buku.value = data[0];
      loading.value = false;
    }
    if (error) {
      throw error;
    }
  } catch (error) {
    console.error("Error fetching book:", error.message);
  }
};

onMounted(() => {
  getBookById();
});
</script>
