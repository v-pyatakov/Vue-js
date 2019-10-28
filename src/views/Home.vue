<template>
  <div class="home">
    <HelloWorld v-bind:msg="name" />
  </div>
</template>

<script>
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'home',
  data:function () {
    return {
      name: 'Home page',
    }},
  components: {
    HelloWorld
  }

}
</script>
