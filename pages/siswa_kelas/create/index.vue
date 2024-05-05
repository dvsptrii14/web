<template>
    <div class="d-flex justify-content-center align-items-center vh-100">
        <div class="card" style="width: 25rem; background-color: #D8EFE9;">
        <form @submit.prevent="submitForm">
  
  <div class="mb-3">
  <label class="form-label p-3 my-0">kelas jurusan id</label>
  <input v-model="formData.kelasjurusan_id" type="text" class="form-control mx-3" style="width: 250px;" id="formGroupExampleInput2" placeholder="masukan kelas jurusan id">
  </div>
  
  <div class="mb-3">
  <label class="form-label p-3 my-0">siswa id</label>
  <input v-model="formData.siswa_id" type="text" class="form-control mx-3" style="width: 250px;" id="formGroupExampleInput2" placeholder="masukan siswa id">
  </div>
  
  <div class="mb-3">
  <label class="form-label p-3 my-0">keterangan</label>
  <input v-model="formData.keterangan" type="text" class="form-control mx-3" style="width: 250px;" id="formGroupExampleInput" placeholder="masukan keterangan">
  </div>
  
    <div class="p-3">
     <button style="border-radius: 10px" type="submit">submit</button>
     <nuxt-link to="/siswa_kelas">
     <button style="border-radius: 10px">kembali</button>
    </nuxt-link>
    </div>
    </form>
    </div>
    </div>
    </template>
  
      <script>
      export default{
  
          data(){
          return{
              formData:{
                  kelasjurusan_id:"",
                  siswa_id:"",
                  keterangan:"",
              }
          }
      },
  
      methods:{
      async submitForm(){
              try{
                  await this.$axios.post("/api/web/siswa_kelas/input", this.formData);
                  alert("data berhasil di input");
                  this.$router.push({
                      name: 'siswa/-kelas'
                  })
              }
              catch(error){
                  console.error("error:",error);
                  alert("data gagal di input");
              }
          }
      },
  
    }
  </script>