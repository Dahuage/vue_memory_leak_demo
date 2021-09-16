<template>
  <div class="home">
    <HelloWorld msg="This hosted by a child compoent! "/>
    <button v-on:click="goAbout">去关于页</button>
    <div id="domNode"></div>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'Home',
  components: {
    HelloWorld
  },
  methods: {
    goAbout: function() {
      this.$router.push({
        path: '/about'
      })
    },

    initDomNode: function() {
      const node = document.createElement('p')
      node.setAttribute('id', 'losted')
      node.innerText = `I am created by vue compoent identified by  [<b>${this._uid}</b>], but I am gonna be a orphan. find me in the heapsnapshot!`
      const container = document.getElementById('domNode')
      container.appendChild(node)
      console.log('Created dom node=', node)
    },

    initDomNodeWithEvent: function() {
      const node = document.createElement('p')
      node.setAttribute('id', 'losted')
      node.innerText = `I am created by vue compoent identified by ${this._uid}, but I am gonna be a orphan.`
      node.onclick = () => {console.log('>>>> DOM BE CLICKED WITHIN', this._uid)}
      const container = document.getElementById('domNode')
      container.appendChild(node)
      console.log('Created dom node=', node)
      // !NOTE: memory leak happens, node HAS REFERS THIS VUE! THIS VUE GONNA NEVER BE RELEASE!
      // !!! What if we do below?
      this.domNode = node  // the node acturally is costomer defined DOM node the memory like be fucked!!!
      // !!! now thing goes more complex and bad, caz we have a circular reference now!
      // !NOTE: lifecyle function `this.beforeDestroy` does not work now!!!!!!
    },

    anotherLeadMomoryLeak: function() {
      // ! As a diy, try it wqq.
      // try it out, do some window level event!
    },
    yetAnotherLeadMomoryLeak: function() {
      // ! As a diy, try it lzs.
      // try it out, do some setTimeout task!
    },
    moreLeadMomoryLeak: function() {
      // ! As a dit, anyone who may intreasted in just try it out.
      // try it out, do some async task& event emmiter or closure programming!
    },
  },
  mounted: function() {
    this.initDomNodeWithEvent();
  },
  beforeDestroy() {
    console.log('Try to destory our made dom node!')
    this.domNode = null
  }
}
</script>
