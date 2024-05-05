<template>
  <div class="content-wrapper">
    <div class="d-flex justify-content-center align-items-center">
      <div class="card" style="width: 25rem; background-color: #d8efe9">
        <form @submit.prevent="submitForm">
          <div class="mb-3">
            <label class="form-label p-3 my-0">Nominal</label>
            <input
              v-model="formData.nominal"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput"
              placeholder="masukan nominal"
            />
          </div>

          <div class="mb-3">
            <label class="form-label p-3 my-0">Tanggal</label>
            <input
              v-model="formData.tanggal"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput2"
              placeholder="masukan tanggal"
            />
          </div>

          <div class="mb-3">
            <label class="form-label p-3 my-0">Jumlah_Tabungan</label>
            <input
              v-model="formData.jumlah_tabungan"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput2"
              placeholder="masukan tabungan"
            />
          </div>

          <div class="mb-3">
            <label class="form-label p-3 my-0">Jumlah_Penarikan</label>
            <input
              v-model="formData.jumlah_penarikan"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput"
              placeholder="masukan jumlah_penarikan"
            />
          </div>

          <div class="mb-3">
            <label class="form-label p-3 my-0">Tanggal_Penarikan</label>
            <input
              v-model="formData.tanggal_penarikan"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput"
              placeholder="masukan tanggal_penarikan"
            />
          </div>

          <div class="mb-3">
            <label class="form-label p-3 my-0">Total_Penarikan</label>
            <input
              v-model="formData.total_penarikan"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput"
              placeholder="masukan total_penarikan"
            />
          </div>

          <div class="mb-3">
            <label class="form-label p-3 my-0">siswa_id</label>
            <input
              v-model="formData.siswa_id"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput"
              placeholder="masukan siswa_id"
            />
          </div>

          <div class="mb-3">
            <label class="form-label p-3 my-0">kelasjurusan_ta_id</label>
            <input
              v-model="formData.kelasjurusan_ta_id"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput"
              placeholder="masukan kelasjurusan_ta_id"
            />
          </div>

          <div class="p-3">
            <button style="border-radius: 10px" type="submit">submit</button>
            <nuxt-link to="/tabungan">
              <button style="border-radius: 10px">kembali</button>
            </nuxt-link>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  layout: "sekolah",
  data() {
    return {
      formData: {
        nominal: "",
        tanggal: "",
        jumlah_tabungan: "",
        jumlah_penarikan: "",
        tanggal_penarikan: "",
        total_penarikan: "",
        siswa_id: "",
        kelasjurusan_ta_id: "",
      },
    };
  },

  methods: {
    async submitForm() {
      try {
        await this.$axios.post("/api/web/tabungan/input", this.formData);
        alert("data berhasil di input");
        this.$router.push({
          name: "Tabungan",
        });
      } catch (error) {
        console.error("error:", error);
        alert("data gagal di input");
      }
    },
  },
};
</script>
