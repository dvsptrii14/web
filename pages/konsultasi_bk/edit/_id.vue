<template>
    <div class="d-flex justify-content-center align-items-center my-5">
        <div class="card" style="width: 25rem; background-color: #D8EFE9;">
        <form @submit.prevent="submitForm">
  
  <div class="mb-3">
  <label class="form-label p-3 my-0">Tujuan Konsultasi</label>
  <input v-model="formData.tujuan" type="text" class="form-control mx-3" style="width: 250px;" id="formGroupExampleInput" placeholder="masukan tujuan konsultasi anda">
  </div>
  
  <div class="mb-3">
  <label class="form-label p-3 my-0">tanggal</label>
  <input v-model="formData.tanggal" type="date" class="form-control mx-3" style="width: 250px;" id="formGroupExampleInput2" placeholder="ex: 2024-10-22">
  </div>
  
  <div class="mb-3">
  <label class="form-label p-3 my-0">Status Konsultasi</label>
  <input v-model="formData.status" type="text" class="form-control mx-3" style="width: 250px;" id="formGroupExampleInput2" placeholder="status jadwal konsultasi">
  </div>
  
  <div class="mb-3">
  <label class="form-label p-3 my-0">Tempat Konsultasi</label>
  <input v-model="formData.tempat" type="text" class="form-control mx-3" style="width: 250px;" id="formGroupExampleInput" placeholder="tempat konsultasi dilaksanakan">
  </div>
  
  <div class="mb-3">
  <label class="form-label p-3 my-0">Jam Konsultasi</label>
  <input v-model="formData.jam" type="time" class="form-control mx-3" style="width: 250px;" id="formGroupExampleInput" placeholder="jam konsultasi dilaksanakan">
  </div>
  
  <div class="mb-3">
  <label class="form-label p-3 my-0">Siswa Kelas id</label>
  <input v-model="formData.siswakelas_id" type="text" class="form-control mx-3" style="width: 250px;" id="formGroupExampleInput" placeholder="id siswa yang konsultasi">
  </div>
  
  <div class="mb-3">
  <label class="form-label p-3 my-0">Guru id</label>
  <input v-model="formData.guru_id" type="text" class="form-control mx-3" style="width: 250px;" id="formGroupExampleInput" placeholder="id guru yang melayani konsultasi">
  </div>

    <div class="p-3">
     <button style="border-radius: 10px" type="submit">submit</button>
     <nuxt-link to="/bacaan">
     <button style="border-radius: 10px">kembali</button>
    </nuxt-link>
    </div>
</form>
<div>
    <b-table striped hover :items = "setKonsultasi_bk" :fields="field">
    <template v-slot:cell(action)="row">
        <b-button :to="{name:'konsultasi_bk-edit-id', params:{id:row.item.id}}">Edit</b-button>
    </template>
    </b-table>
</div>

    </div>
</div>
</template>

<script>
export default{

    data(){
        return{
            formData:{
                tujuan:"",
                 tanggal:"",
                 status:"",
                 tempat:"",
                 jam:"",
                 siswakelas_id:"",
                 guru_id:"",
            }
        }
    },

    mounted() {
      
      //fetching data tag by ID
      this.$axios.get(`/api/web/konsultasi_bk/${this.$route.params.id}`)
        
        .then(response => {
          
          //assing response data to state "menu"
          this.formData.tujuan = response.data.data.tujuan
          this.formData.tanggal = response.data.data.tanggal
          this.formData.status = response.data.data.status
          this.formData.tempat = response.data.data.tempat
          this.formData.jam = response.data.data.jam
          this.formData.siswakelas_id = response.data.data.siswakelas_id
          this.formData.guru_id = response.data.data.guru_id

        })
    },

    methods:{
        async  updateKonsultasi_bk(){
            try{
                await this.$axios.put(`/api/web/konsultasi_bk/update/${this.$route.params.id}`, this.formData);
                alert("berhasil diupdate");
            }
            catch(error){
                console.error("error:",error);
                alert("data gagal dimasukan");
            }
        }
    },
}
</script>