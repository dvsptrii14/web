<template>
  <div class="content-wrapper">
    <div
      class="d-flex justify-content-center align-items-center w-auto bg-success-subtle mx-auto p-"
    >
      <div class="card bg-success-subtle" style="width: 75%">
        <h1 class="mx-3 my-3">Data mata pelajaran</h1>
        <nuxt-link to="/jadwal_pelajaran/create">
          <button style="border-radius: 10px" class="mx-3 my-3">
            Input Data jadwal Pelajaran
          </button>
        </nuxt-link>

        <div>
          <b-table striped hover :items="setJadwal_Pelajaran" :fields="field">
            <template v-slot:cell(action)="row">
              <b-button
                :to="{
                  name: 'Jadwal_Pelajaran-edit-id',
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
        { key: "kelasjurusan_ta_id", label: "kelasjurusan_ta_id" },
        { key: "hari", label: "hari" },
        { key: "pelajaran_id", label: "pelajaran_id" },
        { key: "guru_id", label: "guru_id" },
        { key: "keterangan", label: "keterangan" },
        { key: "action", label: "Action" },
      ],
    };
  },

  methods: {
    async hapusData(id) {
      try {
        await this.$axios.delete(`/api/web/jadwal_pelajaran/delete/${id}`);
        alert("data berhasil dihapus");
        this.$nuxt.refresh();
      } catch (error) {
        console.error("error:", error);
        alert("data gagal dihapus");
      }
    },
  },

  async asyncData({ $axios }) {
    const listData = await $axios.$get("/api/web/jadwal_pelajaran");
    const getJadwal_Pelajaran = listData.data;
    return {
      setJadwal_Pelajaran: getJadwal_Pelajaran.map((item, i) => ({
        id: item.id,
        no: i + 1,
        kelasjurusan_ta_id: item.kelasjurusan_ta_id,
        guru_id: item.guru_id,
        pelajaran_id: item.pelajaran_id,
        hari: item.hari,
        keterangan: item.keterangan,
      })),
    };
  },
};
</script>
