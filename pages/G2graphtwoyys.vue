<template>
  <div id="containerDiv">
    <button @click="handleGraph">点我</button>
  </div>
</template>

<script>
  import axios from 'axios'

  export default {
    methods: {
      async handleGraph () {
        if ($('#myDiv')[0]) {
          return false
        }
        var $container = $("#containerDiv");
        var $myDiv = $('<div>');
        $myDiv.attr('id', 'myDiv');
        $container.append($myDiv);

        const DS = require('@antv/data-set');
        const G2 = require('@antv/g2');

        let {data} = await axios.get('https://api.myjson.com/bins/adh7j');
        var arr = Object.keys(data[0]);
        const ds = new DS.DataSet();
        const dv = ds.createView().source(data);
        dv.transform({
          type: 'fold',
          fields: arr.slice(0, -1), // 展开字段集
          key: '数值', // key字段
          value: 'value', // value字段
        });
        // 定义图表
        const chart = new G2.Chart({
          container: $myDiv[0],
          forceFit: true,
          height: 400
        });
        chart.source(dv);
        chart.axis('转化量', {
          position: 'top',
          label: {
            formatter: val => {
              return val;
            }
          }
        });
        chart.line().position('时间*value').color('数值');
        chart.point().position('时间*vlaue').color('数值').size(4).shape('circle').style({
          stroke: '#fff',
          lineWidth: 1
        });
        chart.render();
      }
    }
  }
</script>
