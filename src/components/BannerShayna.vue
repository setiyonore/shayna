<template>
  <!-- Women Banner Section Begin -->
  <section class="women-banner spad">
    <div class="container-fluid">
      <div class="row">
        <div class="col-lg-12 mt-5" v-if="products.length>0">
          <carousel class="product-slider" :items="3" :nav="false" :autoplay="true" :dots="false">
            <div class="product-item" v-for="itemProduct in products" :key="itemProduct.id">
              <div class="pi-pic">
                <img :src="itemProduct.galeries[0].photo" alt=""/>
                <ul>
                  <li class="w-icon active">
                    <a href="#" @click="saveKeranjang(itemProduct.id,itemProduct.name,itemProduct.price,itemProduct.galeries[0].photo)"><i class="icon_bag_alt"></i></a>
                  </li>
                  <li class="quick-view"><router-link :to="'/product/'+itemProduct.id"> + Quick View</router-link></li>
                </ul>
              </div>
              <div class="pi-text">
                <div class="catagory-name">{{itemProduct.type}}</div>
                <a href="#">
                  <h5>{{ itemProduct.name }}</h5>
                </a>
                <div class="product-price">
                  ${{ itemProduct.price }}
                  <span>$35.00</span>
                </div>
              </div>
            </div>
          </carousel>
        </div>
        <div class="col-lg-12" v-else>
          <p>Data Tidak Ditemukan</p>
        </div>
      </div>
    </div>
  </section>
  <!-- Women Banner Section End -->
</template>

<script>
import carousel from 'vue-owl-carousel';
import axios from 'axios';
export default {
name: "BannerWomenShayna",
  components:{
    carousel,
  },
  data() {
    return {
      products: [],
      keranjangUser: [],
    }
  },
  methods: {
    saveKeranjang(idProduct, nameProduct, priceProduct, photoProduct) {
      var productStored = {
        "id": idProduct,
        "name": nameProduct,
        "price": priceProduct,
        "photo": photoProduct
      }
      this.keranjangUser.push(productStored);
      const parsed = JSON.stringify(this.keranjangUser);
      localStorage.setItem('keranjangUser',parsed);
      window.location.reload();
    }
  },
  mounted() {
  if (localStorage.getItem('keranjangUser')){
    try {
      this.keranjangUser = JSON.parse(localStorage.getItem('keranjangUser'));
    }catch (e) {
      localStorage.removeItem('keranjangUser');
    }
  }
    axios
      .get("http://localhost/shayna-backend/public/api/products")
      .then(res=>(this.products = res.data.data.data))
      .catch(err => console.log(err))
  }
}
</script>

<style scoped>
.product-item{
  margin-right: 25px;

}
</style>
