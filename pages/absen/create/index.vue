<template>
  <div class="content-wrapper">
    <div
      class="d-flex justify-content-center align-items-center w-100 bg-success-subtle mt-5 mb-5"
    >
      <div
        class="card bg-success-subtle"
        style="width: 25rem; background-color: #d8efe9"
      >
        <form @submit.prevent="submitAbsen">
          <div class="mb-3">
            <label class="form-label p-3 my-0">Nama</label>
            <input
              v-model="formData.Nama"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput"
              placeholder="Nama"
            />
          </div>
          <div class="mb-3">
            <label class="form-label p-3 my-0">Kelas</label>
            <input
              v-model="formData.Kelas"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput"
              placeholder="Kelas"
            />
          </div>
          <div class="mb-3">
            <label class="form-label p-3 my-0">Tanggal</label>
            <input
              v-model="formData.tanggal"
              type="date"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput"
              placeholder="Tanggal"
            />
          </div>
          <div class="dropdown show">
            <a
              class="btn btn-secondary dropdown-toggle"
              style="margin-left: 20px"
              href="#"
              role="button"
              id="dropdownMenuLink"
              data-toggle="dropdown"
              aria-haspopup="true"
              aria-expanded="false"
            >
              Daftar Hadir
            </a>
            <div class="dropdown-menu" aria-labelledby="dropdownMenuLink">
              <a class="dropdown-item" href="#">Hadir</a>
              <a class="dropdown-item" href="#">Sakit</a>
              <a class="dropdown-item" href="#">Izin</a>
            </div>
          </div>
          <!-- <div class="mb-3">
  <label class="form-label p-3 my-0">Daftar Hadir</label>
  <input v-model="formData.absensi" type="text" class="form-control mx-3" style="width: 250px"  id="formGroupExampleInput2" placeholder="Absensi">
  </div> -->

          <div class="p-3">
            <button style="border-radius: 10px" type="submit">submit</button>
            <nuxt-link to="/absen">
              <button style="border-radius: 10px">kembali</button>
            </nuxt-link>
          </div>
        </form>
        <div>
          <b-table striped hover :items="setAbesn" :fields="field">
            <template v-slot:cell(action)="row">
              <b-button
                :to="{ name: 'absen-edit-id', params: { id: row.item.id } }"
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

  methods: {
    async submitAbsen() {
      try {
        await this.$axios.post("/api/web/absen/input", this.formData);
        alert("data berhasil di input");
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
