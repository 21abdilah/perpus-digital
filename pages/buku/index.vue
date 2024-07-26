<template>
  <div class="container-fluid">
    <div v-if="loading">Loading data...</div>
    <div v-else>
      <div class="row mt-5">
        <div class="col-md-3 card">
          <form @submit.prevent="getBooks">
            <input
              v-model="keyword"
              type="search"
              class="form-control rounded-5"
              placeholder="mau baca apa hari ini?"
            />
          </form>
        </div>
        <div class="my-3 text-muted">menampilkan {{ books.length }} buku dari {{ books.length }}</div>
        <div class="row">
          <div v-for="(book, i) in books" :key="i" class="col-lg-2">
            <nuxt-link :to="`/buku/${book.id}`">
              <div class="card mb-3">
                <div class="card-body">
                  <img :src="book.cover" class="cover" alt="cover" />
                </div>
              </div>
            </nuxt-link>
          </div>
        </div>
      </div>
    </div>
    <div class="text-center" v-if="!loading && books.length === 0">
      <div class="d-flex justify-content-center align-items-center" style="height: 100vh;">
        <div>
          <h1>😭 Maaf, judul "{{ keyword }}" tidak ditemukan</h1>
          <nuxt-link to="../">
            <button class="btn btn-light btn-lg rounded-4 px-4">KEMBALI</button>
          </nuxt-link>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.btn-light {
  background-color: #5fd8fe !important;
  box-shadow: 1px 1px 10px #5fd8fe !important;
}

.cover {
  width: 100%;
  height: auto;
  object-fit: cover;
  object-position: 0;
}

.card-body {
  box-shadow: 1px 1px 5px black;
}

.bg-warning {
  box-shadow: 1px 1px 10px #E4C72D;
}

button:hover {
  border: 1px solid #0000;
  background-color: #F0FFFF;
  
}
</style>

<script setup>
import { ref, onMounted } from 'vue';
const supabase = useSupabaseClient();

const books = ref([]);
const loading = ref(true);
const keyword = ref('');

const getBooks = async () => {
  loading.value = true;
  const { data, error } = await supabase
    .from("buku")
    .select(`*, kategori(*)`)
    .ilike("judul", `%${keyword.value}%`);
  if (data) books.value = data;
  loading.value = false;
};
const countBook = async () => {
  const { data, count } = await supabase
    .from("buku")
    .select("*", { count: "exact" });
  if (data) book.value = count;
};

onMounted(() => {
  getBooks();
});
</script>
