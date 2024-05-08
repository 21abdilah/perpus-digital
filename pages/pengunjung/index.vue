<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-lg-12">
        <h2 class="text-center my-4">RIWAYAT KUNJUNGAN</h2>
        <div class="my-3">
          <form @submit.prevent="getpengunjung">
            <input
              v-model="keyword"
              type="search"
              class="form-control rounded-5"
              placeholder="Mau baca apa hari ini?"
            />
          </form>
        </div>
        <div class="my-3 text-muted">
          menampilkan {{ visitors.length }} dari {{ jumlah }}
        </div>
        <table class="table">
          <thead>
            <tr>
              <td>#</td>
              <td>NAMA</td>
              <td>KEANGGOTAAN</td>
              <td>WAKTU</td>
              <td>KEPERLUAN</td>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(visitor, i) in visitors" :key="i">
              <td>{{ i + 1 }}</td>
              <td>{{ visitor.nama }}</td>
              <td>{{ visitor.keanggotaan.nama }}</td>
              <td>{{ visitor.tanggal }}, {{ visitor.waktu }}</td>
              <td>{{ visitor.keperluan.nama }}</td>
            </tr>
          </tbody>
        </table>
        <nuxt-link to="../"
          ><button
            class="btn btn-light btn-lg rounded-4 px-4"
            style="float: left"
          >
            KEMBALI
          </button></nuxt-link
        >
        <!-- button -->
        <div class="form-footer">
          <nuxt-link to="/buku"
            ><button class="btn btn-light btn-lg rounded-4 px-4">
              BUKU
            </button></nuxt-link
          >
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
/* CSS for positioning the form footer */
.form-footer {
  position: fixed;
  bottom: 10px; /* adjust as needed */
  right: 0%;
  transform: translateX(-50%);
}
.btn-dark {
  box-shadow: 1px 1px 10px #e4ecea !important;
}
.btn-light {
  background-color: #5fd8fe !important;
  box-shadow: 1px 1px 10px #5fd8fe !important;
}
</style>

<script setup>
const supabase = useSupabaseClient();
const keyword = ref("");
const visitors = ref([]);

const getpengunjung = async () => {
  const { data, error } = await supabase
    .from("pengunjung")
    .select(`*, keanggotaan(*), keperluan(*)`)
    .ilike("nama", `%${keyword.value}%`)
    .order(`id`, { ascending: false });
  if (data) visitors.value = data;
};
const totalPengunjung = async () => {
  const { data, count } = await supabase
    .from("pengunjung")
    .select("*", { count: "exact" });
  if (data) jumlah.value = count;
};
onMounted(() => {
  getpengunjung();
  totalPengunjung();
});
</script>
