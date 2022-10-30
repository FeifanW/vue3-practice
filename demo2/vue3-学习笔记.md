#### 1.toRefs可以把对象变成响应式对象

#### 2.生命周期

vue2里面的beforeDestory  -->  beforeUnmount

​					 destoryed  -->  unmounted

<img src="C:\Users\qihang\AppData\Roaming\Typora\typora-user-images\image-20221029141606534.png" alt="image-20221029141606534" style="zoom:50%;" />

#### 3.侦测变化-watch

watch()第一个参数是要检测变化的值，可以是数组形式同时检测多个

如果想要检测对象中的某一个属性，参数可以写成函数

```js
watch([()=>data.count],()=>{})
```

可以把公共逻辑放到一个hooks文件夹下面，建立对应的ts文件

与mixin相比，很清楚数据的来源、可以设置别名

#### 4.defineComponent

对setup函数进行封装，返回options对象

defineComponent最重要的是，在TypeScript下，给予组件**正确的参数类型推断**

```js
setup(props, context) {}
```

这个context上面提供了三个常用的属性（vue2中挂载在this上面的）attrs、slots、emit

#### 5.Teleport

传送组件

如果一个弹窗组件在深层的子组件中又想在最外层居中，样式不好处理

![image-20221030112221161](C:\Users\qihang\AppData\Roaming\Typora\typora-user-images\image-20221030112221161.png)

比如在深层弹窗子组件外面包裹teleport

```html
<teleport to="#modal">
	<div id="center">
        <h2>this is a modal</h2>
    </div>
</teleport>
```

在外层父组件中可以添加要传送到的节点

```html
<div id="app"></div>
<div id="modal"></div>
```

vue3里面的emit

```js
export default defineComponent({
    emits:{
        'close-modal':null
    },
    setup(props, context){
        const buttonClick = () => {
            context.emit('close-modal')
        }
        return {
            buttonClick
        }
    }
})
```

#### 6.Suspense

异步组件，Suspense里面也可以包裹多个组件

```html
<Suspense>
	<template #default>
        <async-show/>
        <dog-show/>   
    </template>
    <template #fallback>
        <h1>Loading !...</h1>
    </template>
</Suspense>
```

在AsyncShow组件中

```js
import { defineComponent } from 'vue'
export default defineComponent({
    setup() {
        return new Promise((resolve) => {
            setTimeout(() => {
                return resolve({
                    result:42
                })
            },3000)
        })
    }
})
```

捕捉suspense包裹组件的错误可以使用一个钩子函数onErrorCaptured

#### 7.Provide/Inject

provide/inject有点像原来的bus

<img src="C:\Users\qihang\AppData\Roaming\Typora\typora-user-images\image-20221030155606172.png" alt="image-20221030155606172" style="zoom: 80%;" />

发送的地方

```js
provide('名称','要传的数据')
```

在接收的地方

```js
const temp = inject('名称')
```

#### 8.全局API修改

vue2入口文件中是对全局vue对象上的一些属性进行修改，会产生一些问题

- 单元测试全局配置非常容易污染全局环境
- 在不同的apps中，共享一份有不同配置的Vue对象，就会变的很困难

vue3中改成从原来直接修改vue对象，改为修改vue对象的实例

```js
import { createApp } from 'vue'
import App from './App.vue'

const app = createApp(App)
app.use('...')
app.mixin('...')
app.component('...')

app.mount('#app')
```

##### vue3相比vue2修改的api（不全）：

> 全局配置Vue.config -> app.config
>
> config.productionTip被删除
>
> config.ignoredElements改名为config.isCustomElement
>
> config.keyCodes被删除
>
> 全局类注册API
>
> Vue.component -> app.component
>
> Vue.directive -> app.directive
>
> 行为扩展类API
>
> Vue.mixin -> app.mixin
>
> Vue.use -> app.use 

tree shaking机制在es6的export导出之后，如果没有使用，webpack打包的时候就不会打包进去

vue3中全局的api改成具名的导出，就是为了打包的时候可以减少代码
