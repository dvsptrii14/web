<template>
  <div class="content-wrapper">
    <div
      class="d-flex justify-content-center align-items-center w-auto bg-success-subtle mx-3 p-5"
    >
      <div class="card bg-success-subtle" style="width: 75%">
        <h1 class="mx-3 my-3">Data Penulis</h1>
        <nuxt-link to="/penulis/create">
          <button class="mx-3 my-3 rounded">Input Data Penulis</button>
        </nuxt-link>
        <div>
          <b-table striped hover :items="setPenulis" :fields="field">
            <template v-slot:cell(action)="row">
              <b-button
                :to="{ name: 'penulis-edit-id', params: { id: row.item.id } }"
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
        { key: "penulis", label: "Nama penulis" },
        { key: "alamat", label: "Alamat" },
        { key: "telp", label: "Telepon" },
        { key: "action", label: "Action" },
      ],
    };
  },

  methods: {
    async hapusData(id) {
      try {
        await this.$axios.delete(`/api/web/penulis/delete/${id}`);
        alert("data berhasil dihapus");
        this.$nuxt.refresh();
      } catch (error) {
        console.error("error:", error);
        alert("data gagal dihapus");
      }
    },
  },

  async asyncData({ $axios }) {
    const listData = await $axios.$get("/api/web/penulis");
    const getPenulis = listData.data;
    return {
      setPenulis: getPenulis.map((item, i) => ({
        id: item.id,
        no: i + 1,
        penulis: item.penulis,
        alamat: item.alamat,
        telp: item.telp,
      })),
    };
  },
};
</script>
