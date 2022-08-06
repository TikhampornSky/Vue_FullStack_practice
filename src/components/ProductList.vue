<template>
    <router-link :to="{name:'Create'}" class="button is-success mt-5"> เพิ่มรายการสินค้า </router-link>
    <table class="table is-striped is-bordered mt-2 is-fullwidth">
            <thead>
                <tr>
                    <th>Product Name</th>
                    <th>Price</th>
                    <th>Detail</th>
                    <th class="has-text-centered">Actions</th>
                </tr>
            </thead>

            <tbody>
                <tr v-for="item in items" :key="item.product_id ">
                    <td>{{item.product_name}}</td>
                    <td>{{item.product_price}}</td>
                    <td>{{item.product_detail}}</td>
                    <td class="has-text-centered">
                        <router-link :to="{ name: 'Edit', params: { id: item.product_id } }" class="button is-info is-small" > 
                            แก้ไขข้อมูล 
                        </router-link>

                        <a class="button is-danger is-small" @click="deleteProduct(item.product_id)"> 
                            ลบข้อมูล 
                        </a>
                    </td>
                </tr>
            </tbody>
    </table>
</template>

<script>

import axios from "axios";

export default {
    data(){
        return{
            items:[],
        }
    },

    created(){              //When ProductList is called, it will automatically called this function
        this.getProducts()
    },

    methods:{
        //get all product
        async getProducts(){
            try{
                const response = await axios.get("http://localhost:8000/products")          //calling api
                this.items = response.data
            }catch (err) {
                console.log(err)
            }
        },

        //delete product
        async deleteProduct(id){
            try {
                await axios.delete(`http://localhost:8000/products/${id}`)
                this.getProducts()          //Load this page again
            } catch (err) {
                console.log(err)
            }
        }
    }
}
</script>

<style scoped>
    a {
        margin-left: 10px;
    }
</style>