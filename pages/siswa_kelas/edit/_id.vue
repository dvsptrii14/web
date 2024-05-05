<template>
  <div class="content-wrapper">
    <div class="d-flex justify-content-center align-items-center vh-100">
      <div class="card" style="width: 25rem; background-color: #d8efe9">
        <form @submit.prevent="updateSiswa_kelas">
          <div class="mb-3">
            <label class="form-label p-3 my-0">Kelas Jurusan Id</label>
            <input
              v-model="formData.kelasjurusan_id"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput"
              placeholder="masukan kelas jurusan Id"
            />
          </div>

          <div class="mb-3">
            <label class="form-label p-3 my-0">siswa id</label>
            <input
              v-model="formData.siswa_id"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput2"
              placeholder="masukan siswa id"
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
              placeholder="masukan keterangan"
            />
          </div>

          <div class="p-3">
            <button style="border-radius: 10px" type="submit">submit</button>
            <nuxt-link to="/siswa_kelas">
              <button style="border-radius: 10px">kembali</button>
            </nuxt-link>
          </div>
        </form>
        <div>
          <b-table striped hover :items="setSiswa_kelas" :fields="field">
            <template v-slot:cell(action)="row">
              <b-button
                :to="{
                  name: 'siswa_kelas-edit-id',
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
        kelasjurusan_id: "",
        siswa_id: "",
        keterangan: "",
      },
    };
  },

  mounted() {
    //fetching data tag by ID
    this.$axios
      .get(`/api/web/siswa_kelas/${this.$route.params.id}`)

      .then((response) => {
        //assing response data to state "menu"
        this.formData.kelasjurusan_id = response.data.data.kelasjurusan_id;
        this.formData.siswa_id = response.data.data.siswa_id;
        this.formData.keterangan = response.data.data.keterangan;
      });
  },

  methods: {
    async updateSiswa_kelas() {
      try {
        await this.$axios.put(
          `/api/web/siswa_kelas/update/${this.$route.params.id}`,
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
