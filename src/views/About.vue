<template>
  <div class="about">
    <h1>This is an about page</h1>
    <button v-on:click="goHome">回主页</button>
  </div>
</template>

<script>
export default {
  name: 'About',
  methods: {
    goHome: function() {
      this.$router.push({
        path: '/home'
      })
    },
    findLostedDomNode: function() {
      const node = document.getElementById('losted')
      console.log('refounded', node)
      console.log('we got a null though, but the node still lives in memory, the vue hold it as well! ')
    }
  },
  mounted: function() {
    this.findLostedDomNode();
  }
}
</script>
