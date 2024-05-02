<template>
    <div class="d-flex justify-content-center align-items-center vh-100">
        <div class="card" style="width: 25rem; background-color: #D8EFE9;">
        <form @submit.prevent="submitForm">
  
  <div class="mb-3">
  <label class="form-label p-3 my-0">judul</label>
  <input v-model="formData.judul" type="text" class="form-control mx-3" style="width: 250px;" id="formGroupExampleInput" placeholder="masukan judul">
  </div>
  
  <div class="mb-3">
  <label class="form-label p-3 my-0">tanggal</label>
  <input v-model="formData.tanggal" type="date" class="form-control mx-3" style="width: 250px;" id="formGroupExampleInput2" placeholder="masukan tanggal">
  </div>
  
  <div class="mb-3">
  <label class="form-label p-3 my-0">deskripsi</label>
  <input v-model="formData.deskripsi" type="text" class="form-control mx-3" style="width: 250px;" id="formGroupExampleInput2" placeholder="masukan deskripsi">
  </div>
  
  <div class="mb-3">
  <label class="form-label p-3 my-0">tempat</label>
  <input v-model="formData.tempat" type="text" class="form-control mx-3" style="width: 250px;" id="formGroupExampleInput" placeholder="masukan tempat">
  </div>

  <div class="mb-3">
  <label class="form-label p-3 my-0">penanggung jawab</label>
  <input v-model="formData.penanggungjawab" type="text" class="form-control mx-3" style="width: 250px;" id="formGroupExampleInput" placeholder="masukan penanggung jawab">
  </div>

  <div class="mb-3">
  <label class="form-label p-3 my-0">kontak</label>
  <input v-model="formData.kontak" type="text" class="form-control mx-3" style="width: 250px;" id="formGroupExampleInput" placeholder="masukan kontak">
  </div>

  
    <div class="p-3">
     <button style="border-radius: 10px" type="submit">submit</button>
     <nuxt-link to="/kalender_event">
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
                  judul:"",
                  tanggal:"",
                  deskripsi :"",
                  tempat:"",
                  penanggungjawab:"",
                  kontak:'',
              }
          }
      },
  
      methods:{
      async submitForm(){
              try{
                  await this.$axios.post("/api/web/kalender_event/input", this.formData);
                  alert("data berhasil di input");
                  this.$router.push({
                      name: 'kalender_event'
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