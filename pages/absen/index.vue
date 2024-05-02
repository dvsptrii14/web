<template>
    <div class="d-flex justify-content-center align-items-center w-auto bg-success-subtle mx-3 p-5" >
      <div class="card bg-success-subtle" style="width: 75%;"> 
        <h1 class="mx-3 my-3">Data Absen</h1>
        <nuxt-link to="/penulis/create">
          <button class="mx-3 my-3 rounded" >Input Data Absen</button>
        </nuxt-link>
        <div>

          <b-table striped hover :items = "setAbsen" :fields="field">
            <template v-slot:cell(action)="row">
              <b-button :to="{name:'absen-edit-id', params:{id:row.item.id}}">Edit</b-button>
              <b-button @click="hapusData(row.item.id)" variant="danger">Delete</b-button>
            </template>
          </b-table>
        </div>
      </div>
    </div>
</template>

<script>
export default{
  data() {
    return{
   

      field:[
        {key:'no', label:'Nomer'},
        {key:"tanggal", label:"tanggal"},
        {key:"kelasjurusan_ta_id", label:"kelasjurusan_ta_id"},
        {key:"siswakelas_id", label:"siswakelas_id"},
        {key:"absensi", label:"absen"},
        {key:"keterangan", label:"keterangan"},
        {key:"action", label:"Action"},
      ]
    }
  },

  methods:{
async hapusData(id){
  try{
    await this.$axios.delete(`/api/web/absen/delete/${id}`);
    alert("data berhasil dihapus");
    this.$nuxt.refresh()
  }
  catch(error){
        console.error("error:", error);
        alert("data gagal dihapus");
      }
}
  },
 
  async asyncData({$axios}){
    const listData = await $axios.$get("/api/web/absen");
    const getAbsen = listData.data;
    return{
      setAbsen: getAbsen.map((item,i) => ({
        id:item.id,
        no:i+1,
        tanggal:item.tanggal,
        kelasjurusan_ta_id:item.kelasjurusan_ta_id,
        siswakelas_id:item.siswakelas_id,
        absensi:item.absensi,
        keterangan:item.keterangan,
      }))
    };
  },
}
</script>