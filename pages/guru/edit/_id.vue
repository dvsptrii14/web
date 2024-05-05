<template>
  <div class="content-wrapper">
    <div class="d-flex justify-content-center align-items-center vh-100">
      <div class="card" style="width: 25rem; background-color: #d8efe9">
        <form @submit.prevent="updateGuru">
          <div class="mb-3">
            <label class="form-label p-3 my-0">Nama Guru</label>
            <input
              v-model="formData.nama"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput"
              placeholder="masukan nama guru"
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
            <label class="form-label p-3 my-0">Email</label>
            <input
              v-model="formData.email"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput2"
              placeholder="masukan email"
            />
          </div>

          <div class="mb-3">
            <label class="form-label p-3 my-0">Telepon</label>
            <input
              v-model="formData.telepon"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput"
              placeholder="masukan telepon"
            />
          </div>
          <div class="p-3">
            <button style="border-radius: 10px" type="submit">submit</button>
            <nuxt-link to="/guru">
              <button style="border-radius: 10px">kembali</button>
            </nuxt-link>
          </div>
        </form>
        <div>
          <b-table striped hover :items="setGuru" :fields="field">
            <template v-slot:cell(action)="row">
              <b-button
                :to="{ name: 'guru-edit-id', params: { id: row.item.id } }"
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
        nama: "",
        alamat: "",
        email: "",
        telepon: "",
      },
    };
  },

  mounted() {
    //fetching data tag by ID
    this.$axios
      .get(`/api/web/guru/${this.$route.params.id}`)

      .then((response) => {
        //assing response data to state "menu"
        this.formData.nama = response.data.data.nama;
        this.formData.alamat = response.data.data.alamat;
        this.formData.email = response.data.data.email;
        this.formData.telepon = response.data.data.telepon;
      });
  },

  methods: {
    async updateGuru() {
      try {
        await this.$axios.put(
          `/api/web/guru/update/${this.$route.params.id}`,
          this.formData
        );
        alert("berhasil diupdate");
      } catch (error) {
        console.error("error:", error);
        alert("data gagal dimasukan");
      }
    },
  },
};
</script>
