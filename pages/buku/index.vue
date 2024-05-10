<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-lg-12">
        <div class="my-3">
          <form @submit.prevent="getBooks">
            <input
              v-model="keyword"
              type="search"
              class="form-control rounded-5"
              placeholder="mau baca apa hari ini?"
            />
          </form>
        </div>
        <div class="my-3 text-muted">menampilkan {{ books.length }} buku</div>
        <div class="row justify-content-evenly">
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
    <nuxt-link
      to="/"
      class="btn btn-light btn-lg rounded-4 px-4"
      style="margin-top: 10px"
      >KEMBALI</nuxt-link
    >
  </div>
</template>

<script setup>
const supabase = useSupabaseClient();
const book = ref([]);
const keyword = ref([]);
const books = ref([]);

const getBooks = async () => {
  const { data, error } = await supabase
    .from("buku")
    .select(`*, kategori(*)`)
    .ilike("judul", `%${keyword.value}%`);
  if (data) books.value = data;
};

const countBook = async () => {
  const { data, count } = await supabase
    .from("buku")
    .select("*", { count: "exact" });
  if (data) books.value = count;
};

onMounted(() => {
  getBooks();
  countBook();
});
</script>

<style scoped>
.card-body {
  width: 100%;
  height: 20em;
  padding: 0;
}
. {
  widows: 100%;
  height: 100%;
  object-fit: ;
  object-position: 0 30;
}
.btn-dark {
  box-shadow: 1px 1px 10px #e4ecea !important;
}
.btn-light {
  background-color: #5fd8fe !important;
  box-shadow: 1px 1px 10px #5fd8fe !important;
}

</style>
