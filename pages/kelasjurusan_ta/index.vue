<template>
    <div class="d-flex justify-content-center align-items-center w-auto bg-success-subtle mx-3 p-5" >
      <div class="card bg-success-subtle" style="width: 75%;"> 
        <h1 class="mx-3 my-3">Data Penulis</h1>
        <nuxt-link to="/penulis/create">
          <button class="mx-3 my-3 rounded" >Input Data Kelas Jurusan TA</button>
        </nuxt-link>
        <div>

          <b-table striped hover :items = "setPenulis" :fields="field">
            <template v-slot:cell(action)="row">
              <b-button :to="{name:'penulis-edit-id', params:{id:row.item.id}}">Edit</b-button>
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
        {key:"tahun_ajaran", label:"Tahun ajaran"},
        {key:"semester", label:"Semester"},
        {key:"kelas", label:"Kelas"},
        {key:"jurusan_id", label:"jurusan_id"},
        {key:"guru_id", label:"guru_id"},
        {key:"action", label:"Action"},
      ]
    }
  },

  methods:{
async hapusData(id){
  try{
    await this.$axios.delete(`/api/web/kelasjurusan_ta/delete/${id}`);
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
    const listData = await $axios.$get("/api/web/kelasjurusan_ta");
    const getKelasjurusan_ta = listData.data;
    return{
      setPenulis: getKelasjurusan_ta.map((item,i) => ({
        id:item.id,
        no:i+1,
        tahun_ajaran:item.tahun_ajaran,
        semester:item.semester,
        kelas:item.kelas,
        jurusan_id:item.jurusan_id,
        guru_id:item.guru_id,
      }))
    };
  },
}
</script>