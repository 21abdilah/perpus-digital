<template>
  <div class="container-fluid p-5">
    <div class="row">
      <div class="col-lg-12">
        <h2 class="text-center my-4">ISI BUKU KUNJUNGAN</h2>
        <form @submit.prevent="kirimData">
          <div class="mb-3"></div>
          <input
            v-model="form.nama"
            type="text"
            class="form-control form-control-lg rounded-5"
            placeholder="NAMA.."
          /><br />
          <div class="mb-3">
            <select
              v-model="form.keanggotaan"
              class="form-control form-control-lg form-select rounded-5"
            >
              <option value="">KEANGGOTAAN</option>
              <option
                v-for="(member, i) in members"
                :key="i"
                :value="member.id"
              >
                {{ member.nama }}
              </option></select
            ><br />
            <div class="mb-3" v-if="form.keanggotaan == '1'">
              <div class="row">
                <div class="col-md-4">
                  <select
                    v-model="form.tingkat"
                    class="form-control form-control-lg form-select rounded-5 mb-2"
                  >
                    <option value="">TINGKAT</option>
                    <option value="X">X</option>
                    <option value="XI">XI</option>
                    <option value="XII">XII</option>
                  </select>
                </div>
                <div class="col-md-4">
                  <select
                    v-model="form.jurusan"
                    class="form-control form-control-lg form-select rounded-5 mb-2"
                  >
                    <option value="">JURUSAN</option>
                    <option value="PPLG">PPLG</option>
                    <option value="TJKT">TJKT</option>
                    <option value="TSM">TSM</option>
                    <option value="DKV">DKV</option>
                    <option value="TOI">TOI</option>
                  </select>
                </div>
                <div class="col-md-4">
                  <select
                    v-model="form.kelas"
                    class="form-control form-control-lg form-select rounded-5 mb-2"
                  >
                    <option value="">KELAS</option>
                    <option value="1">1</option>
                    <option value="2">2</option>
                    <option value="3">3</option>
                    <option value="4">4</option>
                  </select>
                </div>
              </div>
            </div>
            <div class="mb-3">
              <select
                v-model="form.keperluan"
                class="form-control form-control-lg form-select rounded-5"
              >
                <option value="">KEPERLUAN</option>
                <option
                  v-for="(item, i) in objectives"
                  :key="i"
                  :value="item.id"
                >
                  {{ item.nama }}
                </option>
              </select>
            </div>
          </div>
            <button
              type="submit"
              class="btn bg-success  btn-lg rounded-4 px-4"
              style="float: left "
            >
              KIRIM
            </button>
      
        </form>
        <!-- Back button -->
        <div class="form-kembali">
          <nuxt-link to="../"
            ><button class="btn btn-danger btn-lg rounded-4 px-4">
              KEMBALI
            </button></nuxt-link
          >
        </div>
        <br />
      </div>
    </div>
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
button:hover {
  border: 1px solid #000;
  background-color: #F0FFFF;
  color: #000;
}
</style>

<script setup>
const supabase = useSupabaseClient();

const members = ref([]);
const objectives = ref([]);

const form = ref({
  nama: "",
  keanggotaan: "",
  tingkat: "",
  jurusan: "",
  kelas: "",
  keperluan: "",
});

const kirimData = async () => {
  // console.log(form.value)
  const { error } = await supabase.from("pengunjung").insert([form.value]);
  if (!error) navigateTo("/pengunjung");
};

const getKeanggotan = async () => {
  const { data, error } = await supabase.from("keanggotaan").select("*");
  if (data) members.value = data;
};

const getKeperluan = async () => {
  const { data, error } = await supabase.from("keperluan").select("*");
  if (data) objectives.value = data;
};

onMounted(() => {
  getKeanggotan();
  getKeperluan();
});
</script>
