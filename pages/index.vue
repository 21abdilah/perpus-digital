<template>
  <div class="container-fluid">
    <div class="row my-5 justify-content-around">
      <div class="col-lg-5">
        <nuxt-link to="/pengunjung/tambah">
          <div class="card bg-pengunjung rounded-5">
            <div class="card-body d-flex justify-content-center align-items-center">
              <h2 style="color: #F0FFFF;">PENGUNJUNG</h2>
            </div>
          </div>
        </nuxt-link>
      </div>
      <div class="col-lg-5">
        <nuxt-link to="/buku">
          <div class="card bg-buku rounded-5">
            <div class="card-body d-flex justify-content-center align-items-center">
              <h2 style="color: #F0FFFF;">CARI BUKU</h2>
            </div>
          </div>
        </nuxt-link>
      </div>
    </div>

    <h2 class="mt-5" style="margin-left: 100px;">STATISTIK</h2>
    <div class="row my-5 justify-content-around">
      <div class="col-lg-5">
        <div class="card bg-spengunjung rounded-5">
          <div class="card-body d-flex justify-content-center align-items-center">
            <h2><span>{{ jml_pengunjung }}</span> Pengunjung</h2>
          </div>
        </div>
      </div>

      <div class="col-lg-5">
        <div class="card bg-sbuku rounded-5">
          <div class="card-body d-flex justify-content-center align-items-center">
            <h2><span>{{ jml_buku }}</span> Buku</h2>
          </div>
        </div>
      </div>
    </div>
  </div>
  <div>
    <div>
      <Statistik></Statistik>
    </div>
  </div>
</template>

<script setup>
const supabase = useSupabaseClient()
const jml_pengunjung = ref(0)
const jml_buku = ref(0)

async function getjml_pengunjung() {
  const { error, data, count } = await supabase
    .from("pengunjung")
    .select('*', { count: 'exact' })
  if (count) jml_pengunjung.value = count
}

async function getjml_buku() {
  const { error, data, count } = await supabase
    .from("buku")
    .select('*', { count: 'exact' })
  if (count) jml_buku.value = count
}

onMounted(() => {
  getjml_pengunjung()
  getjml_buku()
})
</script>

<style scoped>
* {
  text-decoration: none;
}
.card {
  height: 250px;
  box-shadow: 1px 1px 10px #424242;
  margin-top: 10px;
}
.card.bg-pengunjung {
  background-image: url('../assets/img/bg kunjungan.jpeg');
  background-repeat: no-repeat;
  background-position: center center;
  background-size: cover;
  margin-top: 10px;
}
.card.bg-buku {
  background-image: url('../assets/img/bg cari-buku.jpg');
  background-repeat: no-repeat;
  background-position: center center;
  background-size: cover;
  margin-top: 10px;
}
.card-body {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
