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

        // 定义图表
        const DS = require('@antv/data-set');
        const G2 = require('@antv/g2');
        const chart = new G2.Chart({
          container: $myDiv[0],
          forceFit: true,
          height: 500
        });
        let {data} = await axios.get('https://api.myjson.com/bins/ypln3');
        const ds = new DS.DataSet();
        const dv = ds.createView().source(data);
        console.log(dv);
        dv.transform({
          type: 'fold',
          fields: ['Tokyo', 'London'], // 展开字段集
          key: 'city', // key字段
          value: 'temperature', // value字段
        });
        chart.source(dv, {
          month: {
            range: [0, 1]
          }
        });
        chart.line().position('month*temperature').color('city').shape('smooth');
        chart.render();
      }
    }
  }
</script>
