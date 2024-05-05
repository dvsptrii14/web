<template>
  <div class="content-wrapper">
    <div
      class="d-flex justify-content-center align-items-center vh-100 bg-success-subtle"
    >
      <div
        class="card bg-success-subtle"
        style="width: 25rem; background-color: #d8efe9"
      >
        <form @submit.prevent="updatePenerbit">
          <div class="mb-3">
            <label class="form-label p-3 my-0">penerbit</label>
            <input
              v-model="formData.penerbit"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput"
              placeholder="penerbit"
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
              placeholder="alamat"
            />
          </div>
          <div class="mb-3">
            <label class="form-label p-3 my-0">Telepon_kantor</label>
            <input
              v-model="formData.telp_kantor"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput2"
              placeholder="telepon_kantor"
            />
          </div>
          <div class="mb-3">
            <label class="form-label p-3 my-0">Kontak</label>
            <input
              v-model="formData.kontak"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput2"
              placeholder="kontak"
            />
          </div>
          <div class="mb-3">
            <label class="form-label p-3 my-0">Telepon Kontak</label>
            <input
              v-model="formData.telp_kontak"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput2"
              placeholder="telepon kontak"
            />
          </div>
          <div class="p-3">
            <button style="border-radius: 10px" type="submit">submit</button>
            <nuxt-link to="/penerbit">
              <button style="border-radius: 10px" type="submit">kembali</button>
            </nuxt-link>
          </div>
        </form>
        <div>
          <b-table striped hover :items="setPenulis" :fields="field">
            <template v-slot:cell(action)="row">
              <b-button
                :to="{ name: 'penerbit-edit-id', params: { id: row.item.id } }"
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
        penerbit: "",
        alamat: "",
        telp_kantor: "",
        kontak: "",
        telp_kontak: "",
      },
    };
  },

  mounted() {
    //fetching data tag by ID
    this.$axios
      .get(`/api/web/penerbit/${this.$route.params.id}`)

      .then((response) => {
        //assing response data to state "menu"
        this.formData.penerbit = response.data.data.penerbit;
        this.formData.alamat = response.data.data.alamat;
        this.formData.telp_kantor = response.data.data.telp_kantor;
        this.formData.kontak = response.data.data.kontak;
        this.formData.telp_kontak = response.data.data.telp_kontak;
      });
  },

  methods: {
    async updatePenerbit() {
      try {
        await this.$axios.put(
          `/api/web/penerbit/update/${this.$route.params.id}`,
          this.formData
        );
        alert("data berhasil di update");
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
