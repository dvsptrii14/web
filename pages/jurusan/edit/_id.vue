<template>
  <div class="content-wrapper">
    <div
      class="d-flex justify-content-center align-items-center vh-100 bg-success-subtle"
    >
      <div
        class="card bg-success-subtle"
        style="width: 25rem; background-color: #d8efe9"
      >
        <form @submit.prevent="updateJurusan">
          <div class="mb-3">
            <label class="form-label p-3 my-0">jurusan</label>
            <input
              v-model="formData.jurusan"
              type="text"
              class="form-control mx-3"
              style="width: 250px"
              id="formGroupExampleInput"
              placeholder="jurusan"
            />
          </div>

          <div class="p-3">
            <button style="border-radius: 10px" type="submit">submit</button>
            <nuxt-link to="/jurusan">
              <button style="border-radius: 10px" type="submit">kembali</button>
            </nuxt-link>
          </div>
        </form>
        <div>
          <b-table striped hover :items="setJurusan" :fields="field">
            <template v-slot:cell(action)="row">
              <b-button
                :to="{ name: 'jurusan-edit-id', params: { id: row.item.id } }"
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
        jurusan: "",
      },
    };
  },

  mounted() {
    //fetching data tag by ID
    this.$axios
      .get(`/api/web/jurusan/${this.$route.params.id}`)

      .then((response) => {
        //assing response data to state "menu"
        this.formData.jurusan = response.data.data.jurusan;
      });
  },

  methods: {
    async updateJurusan() {
      try {
        await this.$axios.put(
          `/api/web/jurusan/update/${this.$route.params.id}`,
          this.formData
        );
        alert("data berhasil di update");
        this.$router.push({
          name: "jurusan",
        });
      } catch (error) {
        console.error("error:", error);
        alert("data gagal di input");
      }
    },
  },
};
</script>
