<template>
  <div class="content-wrapper">
    <div class="d-flex justify-content-center align-items-center vh-100">
      <div class="card" style="width: 25rem; background-color: #d8efe9">
        <form @submit.prevent="submitForm">
          <div class="mb-3">
            <label class="form-label p-3 my-0">Nama penerbit</label>
            <input
              v-model="formData.penerbit"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput"
              placeholder="masukan nama penerbit"
            />
          </div>

          <div class="mb-3">
            <label class="form-label p-3 my-0">Alamat</label>
            <input
              v-model="formData.alamat"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput2"
              placeholder="masukan alamat"
            />
          </div>

          <div class="mb-3">
            <label class="form-label p-3 my-0">telepon kantor</label>
            <input
              v-model="formData.telp_kantor"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput2"
              placeholder="masukan telepon_kantor"
            />
          </div>

          <div class="mb-3">
            <label class="form-label p-3 my-0">Kontak</label>
            <input
              v-model="formData.kontak"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput"
              placeholder="masukan kontak"
            />
          </div>

          <div class="mb-3">
            <label class="form-label p-3 my-0">Telepon Kontak</label>
            <input
              v-model="formData.telp_kontak"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput"
              placeholder="masukan telepon kontak"
            />
          </div>

          <div class="p-3">
            <button style="border-radius: 10px" type="submit">submit</button>
            <nuxt-link to="/penerbit">
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
        penerbit: "",
        alamat: "",
        telp_kantor: "",
        kontak: "",
        telp_kontak: "",
      },
    };
  },

  methods: {
    async submitForm() {
      try {
        await this.$axios.post("/api/web/penerbit/input", this.formData);
        alert("data berhasil di input");
        this.$router.push({
          name: "penerbit",
        });
      } catch (error) {
        console.error("error:", error);
        alert("data gagal di input");
      }
    },
  },
};
</script>
