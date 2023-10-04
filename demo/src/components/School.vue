<template>
  <div class="hello">
    <h1>学校信息（子组件）：</h1>

    <div v-for="item in school" :key="item.name">{{ item }}</div>
    <h3>我是父组件的数据：{{ appName }}</h3>
    <button @click="btnclik">向父组件传递数据</button>
    <button @click="btn">通过$parent获取父组件的数据</button>
    <h3>我通过$parent获取父组件的数据：{{ parent }}</h3>

    <h3>我通过$bus.$emit全局总线获取student组件的数据：{{ student }}</h3>

    <Sudent/>

    <button @click="btnClose">关闭全局事件总线的数据</button>

  </div>
</template>

<script>
import Sudent from './Sudent'
export default {
  name: 'School',
  props:['appName'],
  components: {
    Sudent
  },
  data () {
    return {
      parent: '',
      school: [
        {
          name: '野鸡学院',
          address:'福建'
        },
        {
          name: '贵州大学',
          address: '贵阳'
        },
        {
          name: '清华大学',
          address: '北京'
        }
      ],
      student: [],
    }
  },
  methods: {
    //子组件向父组件传值
    btnclik() {
      this.$emit('send-msg', this.school)  //send-msg为自定义的绑定事件，this.school为向父组件传递的数据
    },
    btn() {
      console.log(this.$parent);  //子组件通过$parent获取父组件的数据
      this.parent = this.$parent.parentName
    },
    btnClose() {
      this.$bus.$off('hello') //关闭
    }
  },
  mounted() {
     console.log("school组件", this)
    this.$bus.$on('hello', (data) => { 
      console.log("School获取学生信息",data);
      this.student = data

     
    })
  },
  beforeDestroy() {
    this.$bus.$off('hello') //关闭
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.hello{
  background-color: rgb(206, 15, 15);
  padding: 50px 50px;
}
</style>
