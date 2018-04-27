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
        const {DataView} = DS.DataSet;
        const dv = new DS.DataView();

        let {data} = await axios.get('https://api.myjson.com/bins/19ntgn');
        var arr = Object.keys(data[0]);
        var xxx = arr[1];
        var yyy = arr[0];
        dv.source(data).transform({
          type: 'percent',
          field: yyy,
          dimension: xxx,
          as: 'percent'
        });
        const chart = new G2.Chart({
          container: $myDiv[0],
          forceFit: true,
          height: 400,
        });
        chart.source(dv, {
          percent: {
            formatter: val => {
              val = parseInt(val * 100) + '%';
              return val;
            }
          }
        });
        chart.coord('theta', {
          radius: 0.75
        });
        chart.tooltip({
          showTitle: false,
          itemTpl: '<li><span style="background-color:{color};" class="g2-tooltip-marker"></span>{name}: {value}</li>'
        });
        chart.intervalStack()
          .position('percent')
          .color(xxx)
          .label('percent', {
            formatter: (val, item) => {
              console.log(item.point);
              return item.point[xxx] + ': ' + item.point[yyy];
            }
          })
          .tooltip(yyy + '*' + xxx, (xxx, yyy) => {
            return {
              name: xxx,
              value: yyy
            };
          })
          .style({
            lineWidth: 1,
            stroke: '#fff'
          });
        chart.render();
        return false
      }
    }
  }

</script>

