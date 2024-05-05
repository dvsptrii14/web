<template>
  <div class="content-wrapper">
    <div
      class="d-flex justify-content-center align-items-center vh-100 bg-success-subtle"
    >
      <div
        class="card bg-success-subtle"
        style="width: 25rem; background-color: #d8efe9"
      >
        <form @submit.prevent="updateCatatan">
          <div class="mb-3">
            <label class="form-label p-3 my-0">Judul</label>
            <input
              v-model="formData.judul"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput"
              placeholder="judul"
            />
          </div>
          <div class="mb-3">
            <label class="form-label p-3 my-0">Tanggal</label>
            <input
              v-model="formData.tanggal"
              type="date"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput2"
              placeholder="tanggal"
            />
          </div>
          <div class="mb-3">
            <label class="form-label p-3 my-0">isi</label>
            <input
              v-model="formData.isi"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput2"
              placeholder="isi"
            />
          </div>
          <div class="mb-3">
            <label class="form-label p-3 my-0">siswakelas_id</label>
            <input
              v-model="formData.siswakelas_id"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput2"
              placeholder="siswakelas_id"
            />
          </div>

          <div class="p-3">
            <button style="border-radius: 10px" type="submit">submit</button>
            <nuxt-link to="/catatan">
              <button style="border-radius: 10px" type="submit">kembali</button>
            </nuxt-link>
          </div>
        </form>
        <div>
          <b-table striped hover :items="setCatatan" :fields="field">
            <template v-slot:cell(action)="row">
              <b-button
                :to="{ name: 'test-edit-id', params: { id: row.item.id } }"
                >Edit</b-button
              >
            </template>
          </b-table>
        </div>
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
        tanggal: "",
        isi: "",
        siswakelas_id: "",
      },
    };
  },

  mounted() {
    //fetching data tag by ID
    this.$axios
      .get(`/api/web/catatan/${this.$route.params.id}`)

      .then((response) => {
        //assing response data to state "menu"
        this.formData.judul = response.data.data.judul;
        this.formData.tanggal = response.data.data.tanggal;
        this.formData.isi = response.data.data.isi;
        this.formData.siswakelas_id = response.data.data.siswakelas_id;
      });
  },

  methods: {
    async updateCatatan() {
      try {
        await this.$axios.put(
          `/api/web/catatan/update/${this.$route.params.id}`,
          this.formData
        );
        alert("data berhasil di update");
        this.$router.push({
          name: "catatan",
        });
      } catch (error) {
        console.error("error:", error);
        alert("data gagal di input");
      }
    },
  },
};
</script>
