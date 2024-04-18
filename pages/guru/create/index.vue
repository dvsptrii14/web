<template>
    <div class="d-flex justify-content-center align-items-center vh-100">
        <div class="card" style="width: 25rem; background-color: #D8EFE9;">
        <form @submit.prevent="submitForm">
  
  <div class="mb-3">
  <label class="form-label p-3 my-0">Nama Guru</label>
  <input v-model="formData.nama" type="text" class="form-control mx-3" style="width: 250px;" id="formGroupExampleInput" placeholder="masukan nama guru">
  </div>
  
  <div class="mb-3">
  <label class="form-label p-3 my-0">Alamat</label>
  <input v-model="formData.alamat" type="text" class="form-control mx-3" style="width: 250px;" id="formGroupExampleInput2" placeholder="masukan alamat">
  </div>
  
  <div class="mb-3">
  <label class="form-label p-3 my-0">Email</label>
  <input v-model="formData.email" type="text" class="form-control mx-3" style="width: 250px;" id="formGroupExampleInput2" placeholder="masukan email">
  </div>
  
  <div class="mb-3">
  <label class="form-label p-3 my-0">Telepon</label>
  <input v-model="formData.telepon" type="text" class="form-control mx-3" style="width: 250px;" id="formGroupExampleInput" placeholder="masukan telepon">
  </div>
  
    <div class="p-3">
     <button style="border-radius: 10px" type="submit">submit</button>
     <nuxt-link to="/guru">
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
                  nama:"",
                  alamat:"",
                  email:"",
                  telepon:"",
              }
          }
      },
  
      methods:{
      async submitForm(){
              try{
                  await this.$axios.post("/api/web/guru/input", this.formData);
                  alert("data berhasil di input");
                  this.$router.push({
                      name: 'guru'
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