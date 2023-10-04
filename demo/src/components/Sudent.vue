<template>
  <div class="hello">
    <h1>学生信息（子组件）：</h1>
    

    <div v-for="item in student" :key="item.id">{{ item }}</div>
   
    <h3>我是父组件的数据：{{ appName }}</h3>

    <button @click="sendStudentName">通过全局事件总线$bus把学生信息给School组件</button>
    <button @click="btn">获取父组件app的数据</button>

    <h3>我是通过$parent获取父组件的数据：{{ parent }}</h3>
    <h3 v-if="parentName">我是通过全局事件总线获取父组件的数据：{{ parentName }}</h3>
  </div>
</template>

<script>
export default {
  name: 'Sudent',
  props: ['appName'],
  data () {
    return {
      student: [
        {
        name: '张三',
        age: '18',
        sex: '男',
        },
      {
          name: '李四',
          age: '19',
          sex: '男',
      },
        {
          name: '王五',
          age: '20',
          sex: '男',
        }

      ],
      parent: '',
      parentName: '',
    }
  },
  methods: {
    sendStudentName() {
      this.$bus.$emit('hello', this.student)
    },
    btn() {
      console.log('student',this.$parent);  //子组件通过$parent获取父组件的数据
      this.parent = this.$parent.parentName
    },
  },
   mounted() {
    this.$bus.$on('app', (data) => {
      console.log("student获取app父组件的信息", data);
      this.parentName = data
      this.parent = data

      console.log(`空字符串为false?,${'' == false}`);

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
  background-color: rgb(19, 141, 84);
  padding: 50px 50px;
}
</style>
