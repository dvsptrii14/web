<template>
  <div class="content-wrapper">
    <div class="d-flex justify-content-center align-items-center vh-100">
      <div class="card" style="width: 25rem; background-color: #d8efe9">
        <form @submit.prevent="submitForm">
          <div class="mb-3">
            <label class="form-label p-3 my-0">Nama jurusan</label>
            <input
              v-model="formData.jurusan"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput"
              placeholder="masukan nama jurusan"
            />
          </div>

          <div class="p-3">
            <button style="border-radius: 10px" type="submit">submit</button>
            <nuxt-link to="/jurusan">
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
        jurusan: "",
      },
    };
  },

  methods: {
    async submitForm() {
      try {
        await this.$axios.post("/api/web/jurusan/input", this.formData);
        alert("data berhasil di input");
        this.$router.push({
          name: "jurusan",
        });
      } catch (error) {
        console.error("error:", error);
        alert("data gagal di input");
      }
    },
  },
};
</script>
