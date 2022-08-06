<template>
  <div style="text-align: center;"> รายการสินค้าใน Database ของท่าน </div>
  <div>
    <div class="field">
      <label class="label">ชื่อสินค้า</label>
      <div class="control">
        <input
          class="input"
          type="text"
          placeholder="ชื่อสินค้า"
          v-model="productName"
        />
      </div>
    </div>

    <div class="field">
      <label class="label">ราคาสินค้า</label>
      <div class="control">
        <input
          class="input"
          type="number"
          placeholder="ราคาสินค้า"
          v-model="productPrice"
        />
      </div>
    </div>

    <div class="field">
      <label class="label">รายละเอียดสินค้า</label>
      <div class="control">
        <input
          class="input"
          type="text"
          placeholder="รายละเอียดสินค้า"
          v-model="productDetail"
        />
      </div>
    </div>

    <div class="control">
      <button class="button is-success" @click="updateProduct">UPDATE</button>
    </div>

  </div>
</template>

<script>

import axios from "axios";

export default {
    data(){
        return{
            productName: "",
            productPrice: 0,
            productDetail:"",
        }
    },
    created: function() {       //When the component is called, the function inside the created will be called
        this.getProductById()
    },
    methods:{
        async getProductById() {
            try {
                const response = await axios.get(`http://localhost:8000/products/${this.$route.params.id}`)
                this.productName = response.data.product_name
                this.productPrice = response.data.product_price
                this.productDetail = response.data.product_detail
            } catch (err) {
                console.log(err)
            }
        },

        //update product
        async updateProduct() {
            try {
                await axios.put(`http://localhost:8000/products/${this.$route.params.id}`, {
                    product_name: this.productName,
                    product_price: this.productPrice,
                    product_detail: this.productDetail
                })
                this.productName = ""
                this.productPrice = 0
                this.productDetail = ""
                this.$router.push("/")
            } catch (err) {
                console.log(err)
            }
        }
    }
}
</script>

<style>

</style>