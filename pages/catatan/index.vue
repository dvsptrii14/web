<template>
    <div class="d-flex justify-content-center align-items-center w-auto bg-success-subtle mx-3 p-5" >
      <div class="card bg-success-subtle" style="width: 75%;"> 
        <h1 class="mx-3 my-3">Data Catatan</h1>
        <nuxt-link to="/catatan/create">
          <button class="mx-3 my-3 rounded" >Input catatan</button>
        </nuxt-link>
        <div>

          <b-table striped hover :items = "setcatatan" :fields="field">
            <template v-slot:cell(action)="row">
              <b-button :to="{name:'catatan-edit-id', params:{id:row.item.id}}">Edit</b-button>
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
        {key:"judul", label:"judul"},
        {key:"tanggal", label:"tanggal"},
        {key:"isi", label:"isi"},
        {key:"siswakelas_id", label:"siswakelas_id"},
        {key:"action", label:"Action"},
      ]
    }
  },

  methods:{
async hapusData(id){
  try{
    await this.$axios.delete(`/api/web/catatan/delete/${id}`);
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
    const listData = await $axios.$get("/api/web/catatan");
    const getCatatan = listData.data;
    return{
      setcatatan: getCatatan.map((item,i) => ({
        id:item.id,
        no:i+1,
        judul:item.judul,
        tanggal:item.tanggal,
        isi:item.isi,
        siswakelas_id:item.siswakelas_id,
      }))
    };
  },
}
</script>