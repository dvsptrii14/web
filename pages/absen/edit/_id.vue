<template>
  <div class="content-wrapper">
    <div
      class="d-flex justify-content-center align-items-center vh-100 bg-success-subtle"
    >
      <div
        class="card bg-success-subtle"
        style="width: 25rem; background-color: #d8efe9"
      >
        <form @submit.prevent="updateAbsen">
          <div class="mb-3">
            <label class="form-label p-3 my-0">Tanggal</label>
            <input
              v-model="formData.tanggal"
              type="date"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput"
              placeholder="tanggal"
            />
          </div>
          <div class="mb-3">
            <label class="form-label p-3 my-0">kelasjururan_ta_id</label>
            <input
              v-model="formData.kelasjurusan_ta_id"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput2"
              placeholder="kelasjurusan_ta_id"
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
          <div class="mb-3">
            <label class="form-label p-3 my-0">Absensi</label>
            <input
              v-model="formData.absensi"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput2"
              placeholder="absensi"
            />
          </div>
          <div class="mb-3">
            <label class="form-label p-3 my-0">Keterangan</label>
            <input
              v-model="formData.keterangan"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput2"
              placeholder="keterangan"
            />
          </div>
          <div class="p-3">
            <button style="border-radius: 10px" type="submit">submit</button>
            <nuxt-link to="/absen">
              <button style="border-radius: 10px" type="submit">kembali</button>
            </nuxt-link>
          </div>
        </form>
        <div>
          <b-table striped hover :items="setAbsen" :fields="field">
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
        tanggal: "",
        kelasjurusan_ta_id: "",
        siswakelas_id: "",
        absensi: "",
        keterangan: "",
      },
    };
  },

  mounted() {
    //fetching data tag by ID
    this.$axios
      .get(`/api/web/absen/${this.$route.params.id}`)

      .then((response) => {
        //assing response data to state "menu"
        this.formData.tanggal = response.data.data.tanggal;
        this.formData.kelasjurusan_ta_id =
          response.data.data.kelasjurusan_ta_id;
        this.formData.siswakelas_id = response.data.data.siswakelas_id;
        this.formData.absensi = response.data.data.absensi;
        this.formData.keterangan = response.data.data.keterangan;
      });
  },

  methods: {
    async updateAbsen() {
      try {
        await this.$axios.put(
          `/api/web/absen/update/${this.$route.params.id}`,
          this.formData
        );
        alert("data berhasil di update");
        this.$router.push({
          name: "absen",
        });
      } catch (error) {
        console.error("error:", error);
        alert("data gagal di input");
      }
    },
  },
};
</script>
