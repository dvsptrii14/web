<template>
  <div class="content-wrapper">
    <div class="d-flex justify-content-center align-items-center vh-100">
      <div class="card" style="width: 25rem; background-color: #d8efe9">
        <form @submit.prevent="submitForm">
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

          <div class="mb-3">
            <label class="form-label p-3 my-0">hari</label>
            <input
              v-model="formData.hari"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput2"
              placeholder="masukan hari"
            />
          </div>

          <div class="mb-3">
            <label class="form-label p-3 my-0">pelajaran id</label>
            <input
              v-model="formData.pelajaran_id"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput2"
              placeholder="masukan pelajaran_id"
            />
          </div>

          <div class="mb-3">
            <label class="form-label p-3 my-0">guru_id</label>
            <input
              v-model="formData.guru_id"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput"
              placeholder="masukan guru_id"
            />
          </div>

          <div class="mb-3">
            <label class="form-label p-3 my-0">keterangan</label>
            <input
              v-model="formData.keterangan"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput"
              placeholder="masukan keterangan"
            />
          </div>

          <div class="p-3">
            <button style="border-radius: 10px" type="submit">submit</button>
            <nuxt-link to="/jadwal_pelajaran">
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
        kelasjurusan_ta_id: "",
        hari: "",
        pelajaran_id: "",
        guru_id: "",
        keterangan: "",
      },
    };
  },

  methods: {
    async submitForm() {
      try {
        await this.$axios.post(
          "/api/web/jadwal_pelajaran/input",
          this.formData
        );
        alert("data berhasil di input");
        this.$router.push({
          name: "Jadwal_Pelajaran",
        });
      } catch (error) {
        console.error("error:", error);
        alert("data gagal di input");
      }
    },
  },
};
</script>
