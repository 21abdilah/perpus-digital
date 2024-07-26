<template>
  <div class="header">
    <div class="h-img">
      <img src="~/assets/img/SMKN4.png" alt="logo smkn 4" />
    </div>
    <div class="h-text">
      <div class="t-judul">
        <h1>PERPUS DIGITAL</h1>
        <address>
          SMKN 4 TASIKMALAYA
          <p>JL.DEPOK,SUKAMENAK,PURBARATU</p>
        </address>
      </div>
    </div>
  </div>
</template>

<style>
.header {
  display: flex;
  align-items: center;
  background-color: #DC143C;
  color: #ffffff;
  padding: 10px;
}

.h-img > img {
  width: 130px;
  height: 130px;
  margin-left: 20px;
}

.t-judul {
  margin-left: 20px;
}

@media (max-width: 750px) {
  .header {
    flex-direction: column;
    align-items: center;
    justify-content: center;
    text-align: center;
  }

  .h-img > img {
    width: 100px;
    height: 100px;
    margin-left: 0;
    margin-bottom: 10px;
  }

  .t-judul {
    margin-left: 0;
  }

  h1 {
    font-size: 1.5em;
  }
}
</style>
