<template>
  <div class="home">
    <HeaderShayna/>
    <HeroWomenShayna/>
    <BannerShayna/>
    <InstaShayna/>
    <PartnerShayna/>
    <FooterShayna/>
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
import FooterShayna from "@/components/FooterShayna";
export default {
  name: 'Home',
  components: {
    // HelloWorld
    HeaderShayna,
    HeroWomenShayna,
    BannerShayna,
    InstaShayna,
    PartnerShayna,
    FooterShayna,

  }
}
</script>
