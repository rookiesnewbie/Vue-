<template>
  <div id="app">
    <h1 ref="title">App父组件</h1>
    <div>{{ parentName }}</div>

    <h5 >子组件传来的数据如下</h5>
    <div v-for="item in message1" :key="item.name">{{ item }}</div>
    <img src="./assets/logo.png">
    <School :appName="parentName" @send-msg="message" ref="content"/>
    <hr>
    <Sudent :appName="parentName" ref="student"/>

    <button @click="receive">通过$ref访问子组件的数据</button>
    <div v-for="item in school" :key="item.name">{{ item }}</div>
      <div v-for="item in sudent" :key="item.name">{{ item }}</div>

    <button @click="sendMessage">通过$bus实现数据共享</button>

  </div>


</template>

<script>
import School from './components/School'
import Sudent from './components/Sudent'

export default {
  name: 'App',
  components: {
    School, Sudent
  },
  data() {
    return {
      parentName: 'App',
      message1: {},
      school: [],
      sudent: [],
    }
  },
  
  methods: {
    message(item) {
      console.log("子组件传来的数据", item);
      this.message1 = item
    },
    receive() {
      //$refs是对象类型，默认是一个空对象
      console.log(this.$refs);
      console.log(this.$children);
      this.school = this.$refs.content.school;
      this.sudent = this.$children[1].student
    },

    sendMessage() {
      this.$bus.$emit('app',this.parentName)
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #04172b;
  margin-top: 60px;
  background-color: blue;

  padding: 50px 50px;
}
</style>
