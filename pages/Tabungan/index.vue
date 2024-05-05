<template>
  <div class="content-wrapper">
    <div
      class="d-flex justify-content-center align-items-center w-auto bg-success-subtle mx-auto p-"
    >
      <div class="card bg-success-subtle" style="width: 100%">
        <h1 class="mx-3 my-3">Data Tabungan</h1>
        <nuxt-link to="/Tabungan/create">
          <button style="border-radius: 10px" class="mx-3 my-3">
            Input Data Tabungan
          </button>
        </nuxt-link>

        <div>
          <b-table striped hover :items="setTabungan" :fields="field">
            <template v-slot:cell(action)="row">
              <b-button
                :to="{ name: 'tabungan-edit-id', params: { id: row.item.id } }"
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
        { key: "nominal", label: "nominal" },
        { key: "tanggal", label: "tanggal" },
        { key: "jumlah_tabungan", label: "jumlah_tabungan" },
        { key: "jumlah_penarikan", label: "jumlah_penarikan" },
        { key: "tanggal_penarikan", label: "tanggal_penarikan" },
        { key: "total_penarikan", label: "total_penarikan" },
        { key: "siswa_id", label: "siswa_id" },
        { key: "kelasjurusan_ta_id", label: "kelasjurusan_ta_id" },
        { key: "action", label: "Action" },
      ],
    };
  },

  methods: {
    async hapusData(id) {
      try {
        await this.$axios.delete(`/api/web/tabungan/delete/${id}`);
        alert("data berhasil dihapus");
        this.$nuxt.refresh();
      } catch (error) {
        console.error("error:", error);
        alert("data gagal dihapus");
      }
    },
  },

  async asyncData({ $axios }) {
    try {
      const listData = await $axios.$get("/api/web/tabungan");
      const gettabungan = listData.data;
      return {
        setTabungan: gettabungan.map((item, i) => ({
          id: item.id,
          no: i + 1,
          nominal: item.nominal,
          tanggal: item.tanggal,
          jumlah_tabungan: item.jumlah_tabungan,
          jumlah_penarikan: item.jumlah_penarikan,
          tanggal_penarikan: item.tanggal_penarikan,
          total_penarikan: item.total_penarikan,
          siswa_id: item.siswa_id,
          kelasjurusan_ta_id: item.kelasjurusan_ta_id,
        })),
      };
    } catch (error) {
      console.error(error);
    }
  },
};
</script>
