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
    <input v-model="salary">
  </div>
</template>

<script>
import {reactive,computed, toRef, toRaw, markRaw, customRef,
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

    // let obj = reactive({   
    // let obj = deal({   
    // // let obj = shallowReactive({  
    //   name:'第一名',
    //   firstName:'',
    //   lastName:'',
    //   fullName:'',
    //   detail:{
    //     salary:30
    //   }
    // })
    let salary = deal(10)

    // const info = {age:10};
    // obj.info = markRaw(info)       
    // console.log("obj", obj)

    function deal(value){
      return customRef((track, trigger)=>{
        return {
          get(){
            console.log("有人从自定义deal里读数据了")
            track()
            return value
          },
          set(newValue){
            console.log("有人改数据了",newValue)
            value = newValue   // 重新赋值
            trigger()
          }
        }
      })
    }

    // 数据
    function btn(){
      salary++
      // obj.info.age ++
      // console.log("age", obj.info.age)
    }
    // function add(){
      // const info = {age:10};
      // obj.info = markRaw(info)       
      // console.log("obj", obj)
    // }
    return{
      num,
      // add,
      // obj,
      btn,
      salary
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
