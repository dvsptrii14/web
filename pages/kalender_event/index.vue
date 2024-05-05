<template>
  <div class="content-wrapper">
    <div
      class="d-flex justify-content-center align-items-center w-auto bg-success-subtle mx-auto p-"
    >
      <div class="card bg-success-subtle" style="width: 100%">
        <h1 class="mx-3 my-3">Data kalender event</h1>
        <nuxt-link to="/kalender_event/create">
          <button style="border-radius: 10px" class="mx-3 my-3">
            Input Data jadwal Pelajaran
          </button>
        </nuxt-link>

        <div>
          <b-table striped hover :items="setkalender_event" :fields="field">
            <template v-slot:cell(action)="row">
              <b-button
                :to="{
                  name: 'kalender_event-edit-id',
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
        { key: "judul", label: "judul" },
        { key: "tanggal", label: "tanggal" },
        { key: "deskripsi", label: "deskripsi" },
        { key: "tempat", label: "tempat" },
        { key: "penanggungjawab", label: "penanggungjawab" },
        { key: "kontak", label: "kontak" },
        { key: "action", label: "Action" },
      ],
    };
  },

  methods: {
    async hapusData(id) {
      try {
        await this.$axios.delete(`/api/web/kalender_event/delete/${id}`);
        alert("data berhasil dihapus");
        this.$nuxt.refresh();
      } catch (error) {
        console.error("error:", error);
        alert("data gagal dihapus");
      }
    },
  },

  async asyncData({ $axios }) {
    const listData = await $axios.$get("/api/web/kalender_event");
    const getkalender_event = listData.data;
    return {
      setkalender_event: getkalender_event.map((item, i) => ({
        id: item.id,
        no: i + 1,
        judul: item.judul,
        tanggal: item.tanggal,
        deskripsi: item.deskripsi,
        tempat: item.tempat,
        penanggungjawab: item.penanggungjawab,
        kontak: item.kontak,
      })),
    };
  },
};
</script>
