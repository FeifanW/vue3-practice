<template>
  <!-- <div id="nav"> -->
    <router-link to="/">Home</router-link> |
    <router-link to="/about" >About</router-link>
  <!-- </div> -->
  <router-view/>
</template>
<script>
import {reactive, provide} from 'vue'
export default {
  name: 'App',
  components: {
    
  },
    setup(props,content){
      let x = reactive({
        name:'蟹老板',
        age:'20'
      })
      provide('provide',x)
    return{
      x
    }
  }
}
</script>
<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
