<template>
  <div id="app">
    <div class="btn" @click="caozuoDOM">D3有强大的操作DOM能力</div>
    <h1 v-if="showCZD">First Header</h1>
    <div class="zzt">
      <div>柱状图</div>
      <svg class="bar-chart"></svg>
    </div>
  </div>
</template>

<script>
import * as d3 from 'd3'
export default {
  name: 'app',
  data(){
    return {
      showCZD: false,
      dataset: [10,20,30,40,50]
    }
  },
  mounted() {
    this.drawZzt()
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
    },
    drawZzt(){
      // 定义svg宽度高度以及柱状图间距
      let svgWidth = 200, svgHeight = 100, barPadding = 10;
      // 柱状图的宽度
      let barWidth = svgWidth / this.dataset.length;
      
      // 绘制图形
      let svg = d3.select('svg')
        .attr("width", svgWidth)
        .attr("height", svgHeight);

      let barChar = svg.selectAll('rect')
        .data(this.dataset)
        .enter()
        .append("rect") // 长方形
        .attr("y",d=>svgHeight-d) // 确定y轴
        .attr("height",d => d)  // 设定高度。这里的d是dataset中的每一项数据
        .attr("width", barWidth - barPadding) // 设定宽度
        .attr("transform", (d,i)=>{ // 设定x轴的坐标
          let translate = [barWidth * i,0]
          return "translate(" + translate + ")"
        })
        .attr("fill","#409EFF")

      let text = svg.selectAll("text")
       .data(this.dataset)
       .enter()
       .append("text")
       .text(d => d)
       .attr("y",(d,i)=> svgHeight - d - 5)
       .attr("x",(d,i)=> barWidth * i)
       .attr("fill","#A64c38")

       console.log(text)
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
.zzt{
  border: 1px solid red;
  margin-top:20px;
}
</style>
