<template>
  <div id="containerDiv">
    <button @click="handleGraph">点我</button>
  </div>
</template>

<script>
  import axios from 'axios'

  //      [{
  //      "genre": "Sports",
  //      "sold": 275
  //    }, {
  //      "genre": "Strategy",
  //      "sold": 115
  //    }, {
  //      "genre": "Action",
  //      "sold": 120
  //    }, {
  //      "genre": "Shooter",
  //      "sold": 350
  //    }, {
  //      "genre": "Shooter1",
  //      "sold": 123
  //    }, {
  //      "genre": "Shooter2",
  //      "sold": 432
  //    }, {
  //      "genre": "Shooter3",
  //      "sold": 283
  //    }, {
  //      "genre": "Other",
  //      "sold": 150
  //    }]
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
        let {data} = await axios.get('https://api.myjson.com/bins/1gbfdz');

        const map = {
          Sports: '运动',
          Strategy: '策略',
          Action: '动作类',
          Shooter: '射击类',
          Shooter1: '射击类1',
          Shooter2: '射击类2',
          Shooter3: '射击类3',
          Other: '其他'
        };
        chart.source(data, {
          genre: {
            formatter: val => {
              return map[val];
            }, // **关键代码**：在列定义中调用 formatter 回调函数，
            alias: '游戏种类' // 列定义，定义该属性显示的别名
          },
          sold: {
            alias: '销售量'
          }
        });
        chart.line().position('genre*sold').label('sold');
        chart.render();
      }
    }
  }
</script>
