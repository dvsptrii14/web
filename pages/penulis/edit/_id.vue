<template>
    <div class="d-flex justify-content-center align-items-center vh-100 bg-success-subtle ">
      <div class="card bg-success-subtle " style="width: 25rem; background-color: #D8EFE9;">     
      <form @submit.prevent="updatePenulis">
        <div class="mb-3">
  <label class="form-label p-3 my-0">Nama Penulis</label>
  <input v-model="formData.penulis" type="text" class="form-control mx-3"  style="width: 250px;" id="formGroupExampleInput" placeholder="nama">
</div>
<div class="mb-3">
  <label class="form-label p-3 my-0">Alamat</label>
  <input v-model="formData.alamat" type="text" class="form-control mx-3"  style="width: 250px"   id="formGroupExampleInput2" placeholder="alamat">
</div>
<div class="mb-3">
  <label class="form-label p-3 my-0">Telp</label>
  <input v-model="formData.telp" type="text" class="form-control mx-3" style="width: 250px"  id="formGroupExampleInput2" placeholder="nomor">
</div>
<div class="p-3">
  <button style="border-radius: 10px;" type="submit">submit</button>
  <nuxt-link to="/penulis"> 
  <button style="border-radius: 10px;" type="submit">kembali</button>
  </nuxt-link>
</div>
</form>
<div>
 <b-table striped hover :items = "setPenulis" :fields="field">
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
                penulis:"",
                alamat:"",
                telp:"",
            }
        }
    },

    mounted() {
      
      //fetching data tag by ID
      this.$axios.get(`/api/web/penulis/${this.$route.params.id}`)
        
        .then(response => {
          
          //assing response data to state "menu"
          this.formData.penulis = response.data.data.penulis
          this.formData.alamat = response.data.data.alamat
          this.formData.telp = response.data.data.telp

        })
    },

    methods:{
    async updatePenulis() {
      try {
        await this.$axios.put(`/api/web/penulis/update/${this.$route.params.id}`, this.formData);
        alert("data berhasil di update");
        this.$router.push({
                    name: 'penulis'
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
