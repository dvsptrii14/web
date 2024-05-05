<template>
  <div class="content-wrapper">
    <div
      class="d-flex justify-content-center align-items-center w-auto bg-success-subtle mx-auto p-"
    >
      <div class="card bg-success-subtle" style="width: 90%">
        <h1 class="mx-3 my-3">Data Konsultasi Bimbingan Konseling</h1>
        <nuxt-link to="/konsultasi_bk/create">
          <button style="border-radius: 10px" class="mx-2 my-2">
            Input data konsultasi bk
          </button>
        </nuxt-link>

        <div>
          <b-table striped hover :items="setKonsultasi_bk" :fields="field">
            <template v-slot:cell(action)="row">
              <b-button
                :to="{
                  name: 'konsultasi_bk-edit-id',
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
        { key: "tujuan", label: "Tujuan" },
        { key: "tanggal", label: "Tanggal" },
        { key: "status", label: "Stauts" },
        { key: "tempat", label: "Tempat" },
        { key: "jam", label: "Jam" },
        { key: "siswakelas_id", label: "Siswakelas_id" },
        { key: "guru_id", label: "guru_id" },
        { key: "action", label: "Action" },
      ],
    };
  },

  methods: {
    async hapusData(id) {
      try {
        await this.$axios.delete(`/api/web/konsultasi_bk/delete/${id}`);
        alert("data berhasil dihapus");
        this.$nuxt.refresh();
      } catch (error) {
        console.error("error:", error);
        alert("data gagal dihapus");
      }
    },
  },

  async asyncData({ $axios }) {
    const listData = await $axios.$get("/api/web/konsultasi_bk");
    const getKonsultasi_bk = listData.data;
    return {
      setKonsultasi_bk: getKonsultasi_bk.map((item, i) => ({
        id: item.id,
        no: i + 1,
        tujuan: item.tujuan,
        tanggal: item.tanggal,
        status: item.status,
        tempat: item.tempat,
        jam: item.jam,
        siswakelas_id: item.siswakelas_id,
        guru_id: item.guru_id,
      })),
    };
  },
};
</script>
