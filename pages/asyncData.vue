<template>
  <div>
      <h1>姓名：{{info.name}}</h1>
      <h2>年龄：{{info.age}}</h2>
      <h2>兴趣：{{info.interest}}</h2>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  mounted () {
        $("body").append("1");
    },
  data(){
     return {
         name:'hello World',
     }
  },
  async asyncData(){
      let {data}=await axios.get('https://api.myjson.com/bins/1007nf')
      return {info: data}

  }
}
</script>
