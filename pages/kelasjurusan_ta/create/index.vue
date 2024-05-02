<template>
    <div class="d-flex justify-content-center align-items-center vh-100 bg-success-subtle ">
      <div class="card bg-success-subtle " style="width: 25rem; background-color: #D8EFE9;">     
      <form @submit.prevent="submitKelasjurusan_ta">
        <div class="mb-3">
  <label class="form-label p-3 my-0">Tahun Ajaran</label>
  <input v-model="formData.tahun_ajaran" type="text" class="form-control mx-3"  style="width: 250px;" id="formGroupExampleInput" placeholder="ta">
  </div>
  <div class="mb-3">
  <label class="form-label p-3 my-0">Semester</label>
  <input v-model="formData.semester" type="text" class="form-control mx-3"  style="width: 250px"   id="formGroupExampleInput2" placeholder="semester">
  </div>
  <div class="mb-3">
  <label class="form-label p-3 my-0">Kelas</label>
  <input v-model="formData.kelas" type="text" class="form-control mx-3" style="width: 250px"  id="formGroupExampleInput2" placeholder="kelas">
  </div>
  <div class="mb-3">
  <label class="form-label p-3 my-0">Jurusan_id</label>
  <input v-model="formData.jurusan_id" type="text" class="form-control mx-3" style="width: 250px"  id="formGroupExampleInput2" placeholder="jurusan_id">
  </div>
  <div class="mb-3">
  <label class="form-label p-3 my-0">Guru_id</label>
  <input v-model="formData.guru_id" type="text" class="form-control mx-3" style="width: 250px"  id="formGroupExampleInput2" placeholder="guru_id">
  </div>
  
  <div class="p-3">
    <button style="border-radius: 10px;" type="submit">submit</button>
    <nuxt-link to="/penulis"> 
    <button style="border-radius: 10px;" >kembali</button>
    </nuxt-link>
  </div>
  
  </form>
  <div>
  <b-table striped hover :items = "setKelasjurusan_ta" :fields="field">
  <template v-slot:cell(action)="row">
    <b-button :to="{name:'test-edit-id', params:{id:row.item.id}}">Edit</b-button>
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
              tahun_ajaran:"",
              semester:"",
              kelas:"",
              jurusan_id:"",
              guru_id:"",

          }
      }
     },
  
     methods:{
      async submitKelasjurusan_ta() {
        try {
          await this.$axios.post("/api/web/kelasjurusan_ta/input", this.formData);
          alert("data berhasil di input");
          this.$router.push({
                      name: 'kelasjurusan_ta'
                  })
        }
        catch(error){
          console.error("error:", error);
          alert("data gagal di input");
        }
      }
    },
    
     }
  </script>