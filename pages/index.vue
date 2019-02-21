<template>
  <div>
    <h4>TODOLIST DEMO</h4>
    <br>
    <input placeholder="Input something" type="text" v-model="todoSomething">
    
    <button @click="changeTodoList">Push Todo List</button>

    <ul>
      <li :key="index" v-for="(item,index) in todoList">
        {{ item }}
        <span @click="removeSomething(index)" style="color: orange; cursor: pointer; font-size: 18px; margin-left: 20px">x</span>
      </li>
    </ul>
  </div>
</template>

<script>
/* eslint-disable */

export default {
  data() {
    return {
      todoSomething: '',
      todoList: []
    }
  },

  asyncData({
    isDev,
    route,
    store,
    env,
    params,
    query,
    req,
    res,
    redirect,
    error
  }) {
    // asyncData 在 nuxt.js 的生命周期中, 会自动混入 data 数据, 填充到 ssr 模板中.
    // 用于处理组件渲染需要的数据 (可使用 promise, await、async, object).
    // 以下是使用 object 作为返回对象的处理办法
    return {
      todoList: ['Hello Nuxt']
    }
  },

  methods: {
    changeTodoList() {
      // 验证必填
      if (!this.todoSomething) {
        alert('好像没有任何要做的事情')

        return
      }

      // 验证重复项
      if (this.todoList.indexOf(this.todoSomething) !== -1) {
        alert('重复了, 再仔细看看')

        return
      }

      // 添加 todo list
      this.todoList.push(this.todoSomething)

      // 清空 todo something
      this.todoSomething = ''
    },

    removeSomething(index) {
      // 删除指定项
      this.todoList.splice(index, 1)
    }
  }
}
</script>

<style>
html {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica,
    Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol';
  line-height: 1.5;
  font-size: 1em;
}

body {
  display: flex;
  justify-content: center;
  margin-top: 10%;
}

html,
body {
  height: 100%;
}

::-webkit-input-placeholder {
  color: #cbd0d5;
}

:-ms-input-placeholder {
  color: #cbd0d5;
}

::-ms-input-placeholder {
  color: #cbd0d5;
}

::placeholder {
  color: #cbd0d5;
}

html::after {
  content: '';
  background: linear-gradient(21deg, #10abff, #1beabd);
  height: 3px;
  width: 100%;
  position: absolute;
  left: 0;
  top: 0;
}
</style>