<template>
  <div id="app">
    <div class="btn" @click="caozuoDOM">D3有强大的操作DOM能力</div>
    <h1 v-if="showCZD">First Header</h1>
  </div>
</template>

<script>
import * as d3 from 'd3'
export default {
  name: 'app',
  data(){
    return {
      showCZD: false
    }
  },
  mounted() {
    
  },
  methods: {
    caozuoDOM(){
      this.showCZD = true
      
      // d3.select() d3.selectAll()

      d3.select('h1').style('color','red')
      .attr('class','heading')
      .text('d3有强大的操作DOM能力')

      d3.select('body').append('p').text('hi')
      d3.select('body').append('p').text('hi2')
      d3.selectAll('p').attr('class','pStyle')
    }
  },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} 
.btn{
  padding: 10px;
  width: 60%;
  margin: 0 auto;
  color: white;
  background: #409EFF;
  border-radius: 5px
}
.heading{
  border: 1px solid red
}
.pStyle{
  font-size: 26px
}
</style>
