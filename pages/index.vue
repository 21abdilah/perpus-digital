<template>
  <div class="container-fluid">
    <div class="row my-5">


      <div class="col-lg-6">
        <nuxt-link to="/buku">
          <div class="card bg-buku rounded-5">
            <div class="card-body">
              <h2>Cari Buku</h2>
            </div>
          </div>
        </nuxt-link>
      </div>
    </div>
    <div class="statistik">
      <h1>STATISTIK</h1>
    </div>
    <div class="row my-5">
      <div class="col-lg-6">
        <nuxt-link to="/pengunjung/tambah">
          <div class="card bg-light rounded-5">
            <div class="cardbody">
              <h2>4</h2>
              <h2 class="pt-5 ps-5">Pengunjung</h2>
            </div>
          </div>
        </nuxt-link>
      </div>

      <div class="col-lg-6">
        <nuxt-link to="/buku">
          <div class="card bg-light rounded-5">
            <div class="card-body text">
              <h2>4</h2>
              <h2 class="pt-5 ps-5">Pengunjung</h2>
            </div>
          </div>
        </nuxt-link>
      </div>
    </div>
  </div>
  <div>
    <Chart />
  </div>
</template>

<style scoped>
.card {
  height: 250px;
  box-shadow: 1px 1px 10px #424242;
  margin-top: 15px;
}
.card.bg-pengunjung {
  background-image: url("../assets/img/bg-home-kunjungan.jpeg");
  background-repeat: no-repeat;
  background-position: center center;
  background-size: cover;
}
.card.bg-buku {
  background: url("../assets/img/bg-home-cari-buku.jpg") no-repeat center center;
  background-size: cover;
}
.text {
  display: flex;
  align-items: center;
}
.text > h1 {
  font-size: 7rem;
}
</style>
