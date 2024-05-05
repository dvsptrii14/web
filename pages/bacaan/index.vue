<template>
  <div class="content-wrapper">
    <div
      class="d-flex justify-content-center align-items-center w-auto bg-success-subtle mx-auto p-"
    >
      <div class="card bg-success-subtle" style="width: 90%">
        <h1 class="mx-3 my-3">Data Buku Bacaan</h1>
        <nuxt-link to="/bacaan/create">
          <button style="border-radius: 10px" class="mx-2 my-2">
            Input Buku Bacaan
          </button>
        </nuxt-link>

        <div>
          <b-table striped hover :items="setBacaan" :fields="field">
            <template v-slot:cell(action)="row">
              <b-button
                :to="{ name: 'bacaan-edit-id', params: { id: row.item.id } }"
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
        { key: "judul", label: "judul buku" },
        { key: "penulis_id", label: "penulis id" },
        { key: "terbit", label: "tahun terbit" },
        { key: "isbn", label: "no isbn" },
        { key: "cover", label: "foto cover" },
        { key: "ringkasan", label: "ringkasan" },
        { key: "penerbit_id", label: "penerbit id" },
        { key: "link", label: "link" },
        { key: "action", label: "Action" },
      ],
    };
  },

  methods: {
    async hapusData(id) {
      try {
        await this.$axios.delete(`/api/web/bacaan/delete/${id}`);
        alert("data berhasil dihapus");
        this.$nuxt.refresh();
      } catch (error) {
        console.error("error:", error);
        alert("data gagal dihapus");
      }
    },
  },

  async asyncData({ $axios }) {
    const listData = await $axios.$get("/api/web/bacaan");
    const getBacaan = listData.data;
    return {
      setBacaan: getBacaan.map((item, i) => ({
        id: item.id,
        no: i + 1,
        judul: item.judul,
        penulis_id: item.penulis_id,
        terbit: item.terbit,
        isbn: item.isbn,
        cover: item.cover,
        ringkasan: item.ringkasan,
        penerbit_id: item.penerbit_id,
        link: item.link,
      })),
    };
  },
};
</script>
