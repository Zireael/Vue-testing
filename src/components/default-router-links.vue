<template lang="html">
  <div>
    <ul>
      <router-link :to="{ path: '/', params: {}, query: {}, hash: {} }" exact tag="li" active-class="active-link"><a>Home</a></router-link>
      <router-link :to="{ name: 'link1', params: {arg1: $route.params.arg1}, query: {locale: 'en', a: 100}, hash: '#elID' }" tag="li" active-class="active-link"><a>Link 1</a></router-link>
      <router-link :to="{ name: 'link2:', params: {arg2: $route.params.arg2}, query: {} }" tag="li" active-class="active-link"><a>Link 2</a></router-link>
    </ul>
  </div>
</template>

<script>
export default {
  // data: function() {
  //   return {
  //     argument1: this.$route.params.arg1
  //   }
  // },
  // watch: function (to, from) {
  //   this.argument1 = to.params.arg1
  // },
  // methods: {
  //   routerNavigate: function() {
  //     this.$router.push('/link2:arg1')
  //   }
  // }
}
</script>

<style lang="css">
</style>
