<template>
  <div class="hello">
    <h1>学生信息（子组件）：</h1>
    

    <div v-for="item in student" :key="item.id">{{ item }}</div>
   
    <h3>我是父组件的数据：{{ appName }}</h3>
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

      ]
    }
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
