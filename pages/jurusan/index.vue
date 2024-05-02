<template>
    <div class="d-flex justify-content-center align-items-center w-auto bg-success-subtle mx-auto p-">
        <div class="card bg-success-subtle" style="width: 75%;">
            <h1 class="mx-3 my-3">Data Jurusan</h1>
            <nuxt-link to="/jurusan/create">
                <button style="border-radius: 10px" class="mx-3 my-3">Input Data Jurusan</button>
            </nuxt-link>

<div>
    <b-table striped hover :items = "setJurusan" :fields="field">
    <template v-slot:cell(action)="row">
        <b-button :to="{name:'jurusan-edit-id', params:{id:row.item.id}}">Edit</b-button>
        <b-button @click="hapusData(row.item.id)" variant="danger">Delete</b-button>
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
                {key:'jurusan', label:'Nama Jurusan'},
                {key:'action', label:'Action'},
            ]
        }
    },

    methods:{
        async hapusData(id){
            try{
                await this.$axios.delete(`/api/web/jurusan/delete/${id}`);
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
        const listData = await $axios.$get("/api/web/jurusan");
        const getJurusan = listData.data;
        return{
            setJurusan: getJurusan.map((item,i) => ({
                id: item.id,
                no: i+1,
                jurusan: item.jurusan,
                
            }))
        };
    },
}
</script>