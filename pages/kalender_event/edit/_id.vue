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
            <label class="form-label p-3 my-0">judul</label>
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
            <label class="form-label p-3 my-0">tanggal</label>
            <input
              v-model="formData.tanggal"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput2"
              placeholder="tanggal"
            />
          </div>
          <div class="mb-3">
            <label class="form-label p-3 my-0">deskripsi</label>
            <input
              v-model="formData.deskripsi"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput2"
              placeholder="deskripsi"
            />
          </div>
          <div class="mb-3">
            <label class="form-label p-3 my-0">tempat</label>
            <input
              v-model="formData.tempat"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput2"
              placeholder="tempat"
            />
          </div>
          <div class="mb-3">
            <label class="form-label p-3 my-0">penanggung jawab</label>
            <input
              v-model="formData.penanggungjawab"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput2"
              placeholder="penanggung jawab"
            />
          </div>
          <div class="mb-3">
            <label class="form-label p-3 my-0">kontak</label>
            <input
              v-model="formData.kontak"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput2"
              placeholder="kontak"
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
                  name: 'kalender_event-edit-id',
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
        judul: "",
        tanggal: "",
        deskripsi: "",
        tempat: "",
        penanggungjawab: "",
        kontak: "",
      },
    };
  },

  mounted() {
    //fetching data tag by ID
    this.$axios
      .get(`/api/web/kalender_event/${this.$route.params.id}`)

      .then((response) => {
        //assing response data to state "menu"
        this.formData.judul = response.data.data.judul;
        this.formData.tanggal = response.data.data.tanggal;
        this.formData.deskripsi = response.data.data.deskripsi;
        this.formData.tempat = response.data.data.tempat;
        this.formData.penanggungjawab = response.data.data.penanggungjawab;
        this.formData.kontak = response.data.data.kontak;
      });
  },

  methods: {
    async updatekalender_event() {
      try {
        await this.$axios.put(
          `/api/web/kalender_event/update/${this.$route.params.id}`,
          this.formData
        );
        alert("data berhasil di update");
        this.$router.push({
          name: "kalender_event",
        });
      } catch (error) {
        console.error("error:", error);
        alert("data gagal di input");
      }
    },
  },
};
</script>
