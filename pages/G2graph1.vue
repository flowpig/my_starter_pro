<template>
  <div>
      <div id="myDiv" ref="myDiv"></div>
  </div>
</template>

<script>

  export default {
    mounted () {
      const G2 = require('@antv/g2');
//      const div = $("#myDiv")[0];
//      const div = this.$refs.myDiv;
      const div = document.getElementById("myDiv");
      const chart = new G2.Chart({
        container: div,
        forceFit: true,
        height: 500
      });
      const data = [
        {genre: 'Sports', sold: 275},
        {genre: 'Strategy', sold: 115},
        {genre: 'Action', sold: 120},
        {genre: 'Shooter', sold: 350},
        {genre: 'Shooter1', sold: 123},
        {genre: 'Shooter2', sold: 432},
        {genre: 'Shooter3', sold: 283},
        {genre: 'Other', sold: 150}
      ];   // G2 对数据源格式的要求，仅仅是 JSON 数组，数组的每个元素是一个标准 JSON 对象
      chart.source(data);   //载入数据源
      chart.line().position('genre*sold').color('#5251FF');
//      chart.point().position('genre*sold').color('genre').shape('circle');     // 创建图形语法，绘制柱状图，由 genre 和 sold 两个属性决定图形位置，genre 映射至 x 轴，sold 映射至 y 轴
//      chart.interval().position('genre*sold').color('genre');
      chart.render();   // 渲染图表
    }
  }
</script>
