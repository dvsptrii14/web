<template>
  <div class="content-wrapper">
    <div class="d-flex justify-content-center align-items-center my-5">
      <div class="card" style="width: 25rem; background-color: #d8efe9">
        <form @submit.prevent="submitForm">
          <div class="mb-3">
            <label class="form-label p-3 my-0">Judul Buku</label>
            <input
              v-model="formData.judul"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput"
              placeholder="masukan judul buku"
            />
          </div>

          <div class="mb-3">
            <label class="form-label p-3 my-0">penulis id</label>
            <input
              v-model="formData.penulis_id"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput2"
              placeholder="masukan penulis id"
            />
          </div>

          <div class="mb-3">
            <label class="form-label p-3 my-0">Tahun Terbit</label>
            <input
              v-model="formData.terbit"
              type="date"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput2"
              placeholder="masukan tahun terbit"
            />
          </div>

          <div class="mb-3">
            <label class="form-label p-3 my-0">No ISBN</label>
            <input
              v-model="formData.isbn"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput"
              placeholder="masukan no ISBN"
            />
          </div>

          <div class="mb-3">
            <label class="form-label p-3 my-0">Foto Cover</label>
            <input
              v-model="formData.cover"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput"
              placeholder="masukan judul cover buku"
            />
          </div>

          <div class="mb-3">
            <label class="form-label p-3 my-0">Ringkasan</label>
            <input
              v-model="formData.ringkasan"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput"
              placeholder="masukan ringkasan buku"
            />
          </div>

          <div class="mb-3">
            <label class="form-label p-3 my-0">Penerbit id</label>
            <input
              v-model="formData.penerbit_id"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput"
              placeholder="masukan penerbit id"
            />
          </div>

          <div class="mb-3">
            <label class="form-label p-3 my-0">link</label>
            <input
              v-model="formData.link"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput"
              placeholder="masukan link/pdf buku"
            />
          </div>

          <div class="p-3">
            <button style="border-radius: 10px" type="submit">submit</button>
            <nuxt-link to="/bacaan">
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
        judul: "",
        penulis_id: "",
        terbit: "",
        isbn: "",
        cover: "",
        ringkasan: "",
        penerbit_id: "",
        link: "",
      },
    };
  },

  methods: {
    async submitForm() {
      try {
        await this.$axios.post("/api/web/bacaan/input", this.formData);
        alert("data berhasil di input");
        this.$router.push({
          name: "bacaan",
        });
      } catch (error) {
        console.error("error:", error);
        alert("data gagal di input");
      }
    },
  },
};
</script>
