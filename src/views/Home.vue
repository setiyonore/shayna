<template>
  <div class="home">
    <HeaderShayna/>
    <HeroWomenShayna/>
    <BannerShayna/>
    <InstaShayna/>
    <PartnerShayna/>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import HeaderShayna from "@/components/HeaderShayna";
import HeroWomenShayna from "@/components/HeroWomenShayna";
import BannerShayna from "@/components/BannerShayna";
import InstaShayna from "@/components/InstaShayna";
import PartnerShayna from "@/components/PartnerShayna";
export default {
  name: 'Home',
  components: {
    // HelloWorld
    HeaderShayna,
    HeroWomenShayna,
    BannerShayna,
    InstaShayna,
    PartnerShayna,

  }
}
</script>
