<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>Essential Links</h2>
    <div v-for="item in articles" :key='item.id'>
      {{item.channel}}
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      articles:[]
    }
  },
  created() {
    this.getarticles()
  },
  methods:{
    //异步获取数据：
    getarticles: function(){
      this.$axios.get('/api/articles?type=more&category=home&shown_offset=1524276761019196&first_view=false')
      .then(res => {
           console.log(res)
           console.log(this.articles[0])
           console.log(res.status)
         if(res.status === 200){
          this.articles = res.data.articles
        }
      })
      .catch(function(err){
        if(err.response){
          console.log(err.response)
        }
      })
   }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
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
