<template>
  <div class="content-wrapper">
    <div
      class="d-flex justify-content-center align-items-center w-auto bg-success-subtle mx-auto p-"
    >
      <div class="card bg-success-subtle" style="width: 75%">
        <h1 class="mx-3 my-3">Data Siswa Kelas</h1>
        <nuxt-link to="/siswa_kelas/create">
          <button style="border-radius: 10px" class="mx-2 my-3">
            Input Data Siswa Kelas
          </button>
        </nuxt-link>

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
        { key: "kelasjurusan_id", label: "Kelas Jurusan Id" },
        { key: "siswa_id", label: "Siswa id" },
        { key: "keterangan", label: "Keterangan" },
        { key: "action", label: "Action" },
      ],
    };
  },

  methods: {
    async hapusData(id) {
      try {
        await this.$axios.delete(`/api/web/siswa_kelas/delete/${id}`);
        alert("data berhasil dihapus");
        this.$nuxt.refresh();
      } catch (error) {
        console.error("error:", error);
        alert("data gagal dihapus");
      }
    },
  },

  async asyncData({ $axios }) {
    const listData = await $axios.$get("/api/web/siswa_kelas");
    const getSiswa_kelas = listData.data;
    return {
      setSiswa_kelas: getSiswa_kelas.map((item, i) => ({
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
