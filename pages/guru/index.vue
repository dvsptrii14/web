<template>
    <div class="d-flex justify-content-center align-items-center w-auto bg-success-subtle mx-auto p-">
        <div class="card bg-success-subtle" style="width: 75%;">
            <h1 class="mx-3 my-3">Data Guru</h1>
            <nuxt-link to="/guru/create">
                <button style="border-radius: 10px" class="mx-3 my-3">Input Data Guru</button>
            </nuxt-link>

<div>
    <b-table striped hover :items = "setGuru" :fields="field">
    <template v-slot:cell(action)="row">
        <b-button :to="{name:'guru-edit-id', params:{id:row.item.id}}">Edit</b-button>
        <b-button @click="hapusData(row.item.id)" variants="danger">Delete</b-button>
    </template>
    </b-table>
    </div>
    </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
          
            field:[
                {key:'no', label:'Nomer'},
                {key:'nama', label:'Nama Guru'},
                {key:'alamat', label:'Alamat'},
                {key:'email', label:'Email'},
                {key:'telepon', label:'Telepon'},
                {key:'action', label:'Action'},
            ]
        }
    },

    methods:{
        async hapusData(id){
            try{
                await this.$axios.delete(`/api/web/guru/delete/${id}`);
                alert("data berhasil dihapus");
                this.$nuxt.refresh()
            }
            catch(error){
                console.error("error:",error);
                alert("data gagal dihapus");
            }
        }
    },

    async asyncData({$axios}){
        const listData = await $axios.$get("/api/web/guru");
        const getGuru = listData.data;
        return{
            setGuru: getGuru.map((item,i) => ({
                id: item.id,
                no: i+1,
                nama: item.nama,
                alamat: item.alamat,
                email: item.email,
                telepon: item.telepon,
            }))
        };
    },
}
</script>