<template>
  <div class="content-wrapper">
    <div
      class="d-flex justify-content-center align-items-center vh-100 bg-success-subtle"
    >
      <div
        class="card bg-success-subtle"
        style="width: 25rem; background-color: #d8efe9"
      >
        <form @submit.prevent="updateJadwal_Pelajaran">
          <div class="mb-3">
            <label class="form-label p-3 my-0">kelasjurusan_ta_id</label>
            <input
              v-model="formData.kelasjurusan_ta_id"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput"
              placeholder="kelasjurusan_ta_id"
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
              placeholder="hari"
            />
          </div>
          <div class="mb-3">
            <label class="form-label p-3 my-0">pelajaran_id</label>
            <input
              v-model="formData.pelajaran_id"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput2"
              placeholder="telepon_kantor"
            />
          </div>
          <div class="mb-3">
            <label class="form-label p-3 my-0">guru_id</label>
            <input
              v-model="formData.guru_id"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput2"
              placeholder="kontak"
            />
          </div>
          <div class="mb-3">
            <label class="form-label p-3 my-0">keterangan</label>
            <input
              v-model="formData.keterangan"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput2"
              placeholder="telepon kontak"
            />
          </div>
          <div class="p-3">
            <button style="border-radius: 10px" type="submit">submit</button>
            <nuxt-link to="/jadwal_pelajaran">
              <button style="border-radius: 10px" type="submit">kembali</button>
            </nuxt-link>
          </div>
        </form>
        <div>
          <b-table striped hover :items="setPenulis" :fields="field">
            <template v-slot:cell(action)="row">
              <b-button
                :to="{
                  name: 'jadwal_pelajaran-edit-id',
                  params: { id: row.item.id },
                }"
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
        kelasjurusan_ta_id: "",
        hari: "",
        pelajaran_id: "",
        guru_id: "",
        keterangan: "",
      },
    };
  },

  mounted() {
    //fetching data tag by ID
    this.$axios
      .get(`/api/web/jadwal_pelajaran/${this.$route.params.id}`)

      .then((response) => {
        //assing response data to state "menu"
        this.formData.kelasjurusan_ta_id =
          response.data.data.kelasjurusan_ta_id;
        this.formData.hari = response.data.data.hari;
        this.formData.pelajaran_id = response.data.data.pelajaran_id;
        this.formData.guru_id = response.data.data.guru_id;
        this.formData.keterangan = response.data.data.keterangan;
      });
  },

  methods: {
    async updateJadwal_Pelajaran() {
      try {
        await this.$axios.put(
          `/api/web/jadwal_pelajaran/update/${this.$route.params.id}`,
          this.formData
        );
        alert("data berhasil di update");
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
