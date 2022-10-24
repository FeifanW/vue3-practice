<template>
  <div class="hello">
    <!-- <div>显示数字{{obj.name}}</div> -->
    <slot></slot>
    <button @click="btn">测试按钮</button>
    <!-- <button @click="add">添加按钮</button> -->
    <!-- <input type="text" v-model="obj.firstName">
    <input type="text" v-model="obj.lastName"> -->
    <!-- <span>全名：{{obj.fullName}}</span> -->
    <!-- <span>薪水：{{obj.detail.salary}}</span> -->
    <!-- <input v-model="salary"> -->
    <teleport to='body'>
      <!-- <div>123456测试</div> -->
      <div v-if="testDialog">123456测试</div>
    </teleport>
  </div>
</template>

<script>
import {reactive,computed, toRef, toRaw, markRaw, customRef, inject,
        isRef,isReactive,isReadonly,isProxy,
        toRefs,shallowReactive,shallowRef, readonly, shallowReadonly} from 'vue'
import {ref} from 'vue'
export default {
  name: 'HelloWorld',
  props:['msg'],
  emits:['hello'],
  beforeCreate(){
    console.log("beforeCreate")
  },
  async setup(props,content){
    let testDialog = ref(false)

    // 数据
    function btn(){
      // salary++
      this.testDialog = true
      console.log("测试",testDialog)
    }

    let p = new Promise((resolve,reject)=>{
      setTimeout(()=>{
        resolve({testDialog, btn})
      },3000)
    })

    return await p
    // return{
    //   // num,
    //   testDialog,
    //   // add,
    //   // obj,
    //   btn,
    //   // salary
    // }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
