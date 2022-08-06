<template>
  <div style="text-align: center;">เพิ่มรายการสินค้า</div>
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
      <button class="button is-success" @click="saveProduct">SAVE</button>
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
    methods:{
        //create new product
        async saveProduct() {
            try {
                await axios.post("http://localhost:8000/products", {
                    product_name: this.productName,
                    product_detail: this.productDetail,
                    product_price: this.productPrice
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