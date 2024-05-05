<template>
    <div class="d-flex justify-content-center align-items-center w-auto bg-success-subtle mx-auto p-">
        <div class="card bg-success-subtle" style="width: 75%;">
            <h1 class="mx-3 my-3">Data Penerbit</h1>
            <nuxt-link to="/penerbit/create">
                <button style="border-radius: 10px" class="mx-3 my-3">Input Data Penerbit</button>
            </nuxt-link>

<div>
    <b-table striped hover :items = "setPenerbit" :fields="field">
    <template v-slot:cell(action)="row">
        <b-button :to="{name:'penerbit-edit-id', params:{id:row.item.id}}">Edit</b-button>
        <b-button @click="hapusData(row.item.id)" variants="danger">kk</b-button>
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
                {key:'penerbit', label:'Nama Penerbit'},
                {key:'alamat', label:'Alamat'},
                {key:'telp_kantor', label:'Telepon Kantor'},
                {key:'kontak', label:'Nama Kontak'},
                {key:'telp_kontak', label:'Telp Kontak'},
                {key:'action', label:'Action'},
            ]
        }
    },

    methods:{
        async hapusData(id){
            try{
                await this.$axios.delete(`/api/web/penerbit/delete/${id}`);
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
        const listData = await $axios.$get("/api/web/penerbit");
        const getPenerbit = listData.data;
        return{
            setPenerbit: getPenerbit.map((item,i) => ({
                id: item.id,
                no: i+1,
                penerbit: item.penerbit,
                alamat: item.alamat,
                telp_kantor: item.telp_kantor,
                kontak: item.kontak,
                telp_kontak: item.telp_kontak,
            }))
        };
    },
}
</script>