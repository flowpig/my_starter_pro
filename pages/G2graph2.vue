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
        const G2 = require('@antv/g2');
        const chart = new G2.Chart({
          container: $myDiv[0],
          forceFit: true,
          height: 500
        });
        let {data}=await axios.get('https://api.myjson.com/bins/1gbfdz');
        chart.source(data);
        chart.line().position('genre*sold').color('#5251FF');
        chart.render();
      }
    }
  }
</script>
