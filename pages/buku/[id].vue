<template>
  <div>
    <h2 class="text-start my-4">{{ buku.judul }}</h2>
    <div class="row">
      <div class="col-md-3">
        <div class="card">
          <div class="card-body">
            <span v-if="buku.cover"
              ><img :src="buku.cover" class="buku" :alt="buku.judul"
            /></span>
            <span v-else
              ><img
                src="https://bukukita.com/babacms/displaybuku/67462_f.jpg"
                class="buku"
            /></span>
          </div>
        </div>
      </div>
      <div class="col-md-6">
        <ul class="list-group list-group-flush">
          <li class="list-group-item">penulis : {{ buku.penulis }}</li>
          <li class="list-group-item">
            tahun_terbit : {{ buku.tahun_terbit }}
          </li>
          <li class="list-group-item">rak : {{ buku.rak }}</li>
          <li class="list-group-item">kategori : {{ buku.kategori }}</li>
        </ul>
      </div>
    </div>
    <NuxtLink to="/buku" class="btn btn-light btn-lg rounded-5 px-5">
      kembali
    </NuxtLink>
  </div>
</template>

<script setup>
const router = useRoute();
const id = router.params.id;
const supabase = useSupabaseClient();
const book = ref({});
const loading = ref(true);
onMounted(() => getData());

async function getData() {
  loading.value = true;
  let { data, error } = await supabase
    .from("buku")
    .select(
      `
    id, judul, penulis, penerbit, 
    kategori(id), rak(kode), cover
  `
    )

    .eq("id", id);
  if (data) {
    book.value = data[0];
    loading.value = false;
  }
  if (error) throw error;
}
</script>

<style scoped>
.btn {
  background-color: #c0c0c0;
  position: fixed;
  bottom: 30px;
  right: 30px;
}
.buku {
  width: 100%;
}
</style>
