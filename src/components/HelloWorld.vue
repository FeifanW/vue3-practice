<template>
  <div class="hello">
    <div>显示数字{{obj.name}}</div>
    <slot></slot>
    <button @click="btn">测试按钮</button>
    <button @click="add">添加按钮</button>
    <input type="text" v-model="obj.firstName">
    <input type="text" v-model="obj.lastName">
    <span>全名：{{obj.fullName}}</span>
    <span v-if="obj.info.age">年龄：{{obj.info.age}}</span>
  </div>
</template>

<script>
import {reactive,computed, toRef, toRaw, markRaw,
        toRefs,shallowReactive,shallowRef, readonly, shallowReadonly} from 'vue'
import {ref} from 'vue'
export default {
  name: 'HelloWorld',
  props:['msg'],
  emits:['hello'],
  beforeCreate(){
    console.log("beforeCreate")
  },
  setup(props,content){

    let num = ref(10)

    let obj = reactive({   
    // let obj = shallowReactive({  
      name:'第一名',
      firstName:'',
      lastName:'',
      fullName:'',
      detail:{
        salary:30
      }
    })

    const info = {age:10};
    obj.info = markRaw(info)       
    console.log("obj", obj)

    // 数据
    function btn(){
      obj.info.age ++
      console.log("age", obj.info.age)
    }
    function add(){
      // const info = {age:10};
      // obj.info = markRaw(info)       
      // console.log("obj", obj)
    }
    return{
      num,
      add,
      obj,
      btn,
    }
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
