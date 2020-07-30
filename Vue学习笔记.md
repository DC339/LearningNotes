# Vue学习笔记

## Day1 - router与组件的连接以及页面跳转

#### 1.router与组件的连接

##### 在router - index.js下配置路由设置文件，指定路由对应组件

```js
import Vue from 'vue'
import Router from 'vue-router'
import HelloWorld from '@/components/HelloWorld'
import SelectPage from '@/components/SelectPage'
import SearchPage from '@/components/search-page'

Vue.use(Router)

export default new Router({
  routes: [
    {
      path: '/',
      name: 'HelloWorld',
      component: HelloWorld
    },
    {
      path: '/open',
      name: 'SelectPage',
      component: SelectPage
    },
    {
      path: '/searchPage',
      name: 'searchPage',
      component: SearchPage
    }
  ]
})
```

#### 2.通过router展示页面

```vue
<!--写在想要渲染组件的地方，等组件跳转过来就渲染-->
<router-view/>
```

#### 3.通过router跳转页面

```vue
<!--
to:跳转至目标页面
tag="button"渲染成原生标签，即button标签
-->
<router-link to="./home" tag="button"></router-link>
```

##### ps:在btnPage组件中跳转至另一页面（"/searchPage"）的另一方法：

btnPage.vue组件：

```vue
<!--通过点击事件跳转页面-->
<template>
    <Button @Click="handClick" type="primary">Submit</Button>
</template>
<script>
export default {
    data: {},
    methods: {
        handClick: function () {
            this.$router.replace('/searchPage')
        }
    }
}
</script>
```

！！！注意：页面接口"/searchPage"需要提前在index.js中配置好。

#### 4.在page文件下的组件中引入components中的基础组件（可能是按钮等小组件）

例：在btnPage.vue中引入btn.vue按钮组件

btn.vue

```vue
<template>
    <div>
        <h4>this is a new page</h4>
        <Button type="primary" @click="handClick">submit</Button>
    </div>
</template>

<script>
export default {
    data () {

    },
    methods: {
        handClick: function () {
            this.$router.replace('/searchPage')
        }
    }
}
</script>
```

btnPage.vue

```vue
<template>
    <div>
        <btn></btn>
    </div>
</template>

<script>
import btn from '@/components/btn.vue'
export default {
    components: {btn},
    methods: {}
}
</script>
```

