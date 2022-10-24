<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <!-- <HelloWorld ref="hello" msg="Welcome to Your Vue.js App">
      <span>测试插槽</span>
    </HelloWorld> -->
    <Suspense>
      <template v-slot:default>
        <Child></Child>
      </template>
      <template v-slot:fallback>
        <div>
          没有出现
        </div>
      </template>
    </Suspense>
  </div>
</template>

<script>
// @ is an alias to /src
import { defineAsyncComponent } from 'vue'
const Child =  defineAsyncComponent(()=> import('@/components/HelloWorld.vue'))

export default {
  name: 'Home',
  components: {
    // HelloWorld,
    Child
  },
}
</script>
