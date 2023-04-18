
<template>
    <div class="container mt-4 shadow-lg p-3 mb-5 bg-body rounded"> 
        <table class="table table-bordered table-striped">
            <thead>
                <tr>
                    <th>ID</th>
                    <th>Name</th>
                    <th>phone</th>
                    <th>website</th>
                    <th>city</th>
                </tr>
            </thead>
            <tbody id="data">
                <tr v-for="(data,i) in showData" :key='i' >
                    <td> {{data.id}} </td>
                    <td> {{data.name}} </td>
                    <td> {{data.phone}} </td>
                    <td> {{data.website}} </td>
                    <td> {{data.address.city}} </td>
                </tr>
            </tbody>
        </table>
        <div>
            <button @click="mostrarBack"  class="btn btn-dark mx-4">Atras</button>
            <button  @click="mostrarSig"  class="btn btn-dark">Siguiente</button>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    data(){
        return{
            data: [],
            indice: 0,
            maxn: 2
        }
    },
    methods:{
        mostrarSig(){
            if(this.indice + this.maxn < this.data.length){
                this.indice += this.maxn
            }
        },
        mostrarBack(){
            if(this.indice - this.maxn >= 0){
                this.indice -= this.maxn
            }
        }
     
    },
    mounted(){
        axios.get('https://jsonplaceholder.typicode.com/users')
                .then(res => this.data = res.data)
                .catch(err => console.log(err))
        console.log('ahjskdhaskjdha')
    },
    computed:{
        showData(){
            return this.data.slice(this.indice, this.indice + this.maxn)
        }
    }


}
</script>

<style>

</style>

// <tr> 
//                         <td> ${data[i].id} </td> 
//                         <td> ${data[i].name} </td> 
//                         <td> ${data[i].phone} </td> 
//                         <td> ${data[i].website} </td> 
//                         <td> ${data[i].address.city} </td> 
// </tr>