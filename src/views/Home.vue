<template>
  <div class="home">
    <HeaderShayna/>
    <HeroShayna/>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import HeaderShayna from "@/components/HeaderShayna";
import HeroShayna from "@/components/HeroShayna";
export default {
  name: 'Home',
  components: {
    // HelloWorld
    HeaderShayna,
    HeroShayna,

  }
}
</script>
