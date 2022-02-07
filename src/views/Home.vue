<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld ref="hello" msg="Welcome to Your Vue.js App" @hello="hello">
      <span>测试插槽</span>
    </HelloWorld>
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
  methods:{
    test(){
      console.log("传值成功了！")
    },
    hello(){
      console.log("emit成功了")
    }
  },
  onMounted(){
    this.$refs.hello.$on('clickBtn',test)
  }
}
</script>
