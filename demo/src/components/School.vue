<template>
  <div class="hello">
    <h1>学校信息（子组件）：</h1>

    <div v-for="item in school" :key="item.name">{{ item }}</div>
    <h3>我是父组件的数据：{{ appName }}</h3>
    <button @click="btnclik">向父组件传递数据</button>
    <button @click="btn">通过$parent获取父组件的数据</button>
    <h3>我通过$parent获取父组件的数据：{{ parent }}</h3>
  </div>
</template>

<script>
export default {
  name: 'School',
  props:['appName'],
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
      ]
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
    }
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
