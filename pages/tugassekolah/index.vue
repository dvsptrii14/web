<template>
  <div class="content-wrapper">
    <div
      class="d-flex justify-content-center align-items-center w-auto bg-success-subtle mx-auto p-"
    >
      <div class="card bg-success-subtle" style="width: 75%">
        <h1 class="mx-3 my-3">Data Tugas Sekolah</h1>
        <nuxt-link to="/tugassekolah/create">
          <button style="border-radius: 10px" class="mx-2 my-3">
            Input Data Tugas Sekolah
          </button>
        </nuxt-link>

        <div>
          <b-table striped hover :items="setSiswa_kelas" :fields="field">
            <template v-slot:cell(action)="row">
              <b-button
                :to="{
                  name: 'tugassekolah-edit-id',
                  params: { id: row.item.id },
                }"
                >Edit</b-button
              >
              <b-button @click="hapusData(row.item.id)" variant="danger"
                >Delete</b-button
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
      field: [
        { key: "no", label: "Nomer" },
        { key: "pelajaran_id", label: "Pelajaran ID" },
        { key: "tgl", label: "Tanggal Tugas" },
        { key: "deskripsi", label: "Deskripsi Tugas" },
        { key: "tgl_pengumpulan", label: "Tanggal Pengumpulan" },
        { key: "isi_tugas", label: "Isi Tugas" },
        { key: "siswakelas_id", label: "Siswa Kelas ID" },
        { key: "guru_id", label: "Guru ID" },
        { key: "action", label: "Action" },
      ],
    };
  },

  methods: {
    async hapusData(id) {
      try {
        await this.$axios.delete(`/api/web/tugassekolah/delete/${id}`);
        alert("data berhasil dihapus");
        this.$nuxt.refresh();
      } catch (error) {
        console.error("error:", error);
        alert("data gagal dihapus");
      }
    },
  },

  async asyncData({ $axios }) {
    const listData = await $axios.$get("/api/web/tugassekolah");
    const getTugassekolah = listData.data;
    return {
      setTugassekolah: getTugassekolah.map((item, i) => ({
        id: item.id,
        no: i + 1,
        kelasjurusan_id: item.kelasjurusan_id,
        siswa_id: item.siswa_id,
        keterangan: item.keterangan,
      })),
    };
  },
};
</script>
