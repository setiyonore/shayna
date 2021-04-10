<template>
  <div class="product">
    <HeaderShayna/>
    <!-- Breadcrumb Section Begin -->
    <div class="breacrumb-section text-left">
      <div class="container">
        <div class="row">
          <div class="col-lg-12">
            <div class="breadcrumb-text product-more">
              <router-link to="/"> <i class="fa fa-home"></i> Home</router-link>
              <span>Detail</span>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- Breadcrumb Section Begin -->

    <!-- Product Shop Section Begin -->
    <section class="product-shop spad page-details">
      <div class="container">
        <div class="row">
          <div class="col-lg-12">
            <div class="row">
              <div class="col-lg-6">
                <div class="product-pic-zoom">
                  <img class="product-big-img" :src="gambar_default" alt="" />
                </div>
                <div class="product-thumbs" v-if="productDetails.galeries.length>0">
                  <carousel :dots="false" :nav="false" class="product-thumbs-track ps-slider">
                    <div v-for="image in productDetails.galeries" :key="image.id"
                        class="pt" @click="changeImage(image.photo)" :class="image.photo == gambar_default ? 'active' : '' ">
                      <img :src="image.photo" alt="" />
                    </div>
                  </carousel>
                </div>
              </div>
              <div class="col-lg-6">
                <div class="product-details text-left">
                  <div class="pd-title">
                    <span>{{productDetails.type}}</span>
                    <h3>{{ productDetails.name }}</h3>
                  </div>
                  <div class="pd-desc">
                    <p v-html="productDetails.description"></p>
                    <h4>${{ productDetails.price }}</h4>
                  </div>
                  <div class="quantity">
                    <router-link to="/cart" class="primary-btn pd-cart">
                      <a @click="saveKeranjang(productDetails.id,productDetails.name,productDetails.price,productDetails.galeries[0].photo)" href="#" class="primary-btn pd-cart">Add To Cart</a>
                    </router-link>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
    <!-- Product Shop Section End -->
    <RelatedShayna/>
    <FooterShayna/>
  </div>
</template>

<script>
// @ is an alias to /src
import HeaderShayna from "@/components/HeaderShayna";
import FooterShayna from "@/components/FooterShayna";
import carousel from 'vue-owl-carousel';
import RelatedShayna from "@/components/RelatedShayna";
import axios from "axios";
export default {
  name: 'Product',
  components: {
    // HelloWorld
    HeaderShayna,
    FooterShayna,
    carousel,
    RelatedShayna,

  },
  data(){
    return {
      gambar_default:"",
        thumbs:[],
        productDetails: [],
        keranjangUser:[],
    }
  },
  methods: {
    changeImage(urlImage) {
      this.gambar_default = urlImage;
    },
    setDataPicture(data){
      this.productDetails = data;
      this.gambar_default = data.galeries[0].photo;
    },
    saveKeranjang(idProduct,nameProduct,priceProduct,photoProduct){
      var productStored = {
        "id": idProduct,
        "name": nameProduct,
        "price": priceProduct,
        "photo": photoProduct
      }
      this.keranjangUser.push(productStored);
      const parsed = JSON.stringify(this.keranjangUser);
      localStorage.setItem('keranjangUser', parsed);
    }
  },
  mounted() {
    if (localStorage.getItem('keranjangUser')) {
      try {
        this.keranjangUser = JSON.parse(localStorage.getItem('keranjangUser'));
      } catch(e) {
        localStorage.removeItem('keranjangUser');
      }
    }
    axios
      .get("http://localhost/shayna-backend/public/api/products",{
          params: {
            id: this.$route.params.id
          }
      })
      .then(res => (this.setDataPicture(res.data.data)))
      .catch(err => console.log(err))
  }
}
</script>
<style scoped>
.product-thumbs .pt{
  margin-right: 14px;
}
</style>
