<template>
    <div class="d-flex justify-content-center align-items-center vh-100">
        <div class="card" style="width: 25rem; background-color: #D8EFE9;">
        <form @submit.prevent="submitForm">
  
  <div class="mb-3">
  <label class="form-label p-3 my-0">Judul Buku</label>
  <input v-model="formData.judul" type="text" class="form-control mx-3" style="width: 250px;" id="formGroupExampleInput" placeholder="masukan judul buku">
  </div>
  
  <div class="mb-3">
  <label class="form-label p-3 my-0">penulis id</label>
  <input v-model="formData.penulis_id" type="text" class="form-control mx-3" style="width: 250px;" id="formGroupExampleInput2" placeholder="masukan penulis id">
  </div>
  
  <div class="mb-3">
  <label class="form-label p-3 my-0">Tahun Terbit</label>
  <input v-model="formData.terbit" type="date" class="form-control mx-3" style="width: 250px;" id="formGroupExampleInput2" placeholder="masukan tahun terbit">
  </div>
  
  <div class="mb-3">
  <label class="form-label p-3 my-0">No ISBN</label>
  <input v-model="formData.isbn" type="text" class="form-control mx-3" style="width: 250px;" id="formGroupExampleInput" placeholder="masukan no ISBN">
  </div>
  
  <div class="mb-3">
  <label class="form-label p-3 my-0">Foto Cover</label>
  <input v-model="formData.cover" type="text" class="form-control mx-3" style="width: 250px;" id="formGroupExampleInput" placeholder="masukan judul cover buku">
  </div>
  
  <div class="mb-3">
  <label class="form-label p-3 my-0">Ringkasan</label>
  <input v-model="formData.ringkasan" type="text" class="form-control mx-3" style="width: 250px;" id="formGroupExampleInput" placeholder="masukan ringkasan buku">
  </div>
  
  <div class="mb-3">
  <label class="form-label p-3 my-0">Penerbit id</label>
  <input v-model="formData.penerbit_id" type="text" class="form-control mx-3" style="width: 250px;" id="formGroupExampleInput" placeholder="masukan penerbit id">
  </div>
  
  <div class="mb-3">
  <label class="form-label p-3 my-0">link</label>
  <input v-model="formData.link" type="text" class="form-control mx-3" style="width: 250px;" id="formGroupExampleInput" placeholder="masukan link/pdf buku">
  </div>

    <div class="p-3">
     <button style="border-radius: 10px" type="submit">submit</button>
     <nuxt-link to="/bacaan">
     <button style="border-radius: 10px">kembali</button>
    </nuxt-link>
    </div>
</form>
<div>
    <b-table striped hover :items = "setBacaan" :fields="field">
    <template v-slot:cell(action)="row">
        <b-button :to="{name:'bacaan-edit-id', params:{id:row.item.id}}">Edit</b-button>
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
                judul:'',
                penulis_id:'',
                terbit:'',
                isbn:'',
                cover:'',
                ringkasan:'',
                penerbit_id:'',
                link:'',
            }
        }
    },

    mounted() {
      
      //fetching data tag by ID
      this.$axios.get(`/api/web/bacaan/${this.$route.params.id}`)
        
        .then(response => {
          
          //assing response data to state "menu"
          this.formData.judul = response.data.data.judul
          this.formData.penulis_id = response.data.data.penulis_id
          this.formData.terbit = response.data.data.terbit
          this.formData.isbn = response.data.data.isbn
          this.formData.cover = response.data.data.cover
          this.formData.ringkasan = response.data.data.ringkasan
          this.formData.penerbit_id = response.data.data.penerbit_id
          this.formData.link = response.data.data.link

        })
    },

    methods:{
        async  updateBacaan(){
            try{
                await this.$axios.put(`/api/web/bacaan/update/${this.$route.params.id}`, this.formData);
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