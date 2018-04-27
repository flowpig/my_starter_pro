<template>
  <div>
    <el-row>
      <el-button type="primary" @click="handleMarket" plain>从营销系统获取客户</el-button>
      <el-button type="success" @click="handleTele" plain>从电销系统获取客户</el-button>
    </el-row>
    <el-row :gutter="20">
      <el-col :span="6">
        <span>过滤条件: </span>
        <el-select v-model="value2" placeholder="请选择" clearable @change="handleCustomFilter">
          <el-option
            v-for="item in options2"
            :key="item.value"
            :label="item.label"
            :value="item.value"
            :disabled="item.disabled">
          </el-option>
        </el-select>
      </el-col>
      <el-col :span="5">
        <el-input
          placeholder="请输入内容"
          v-model="input10"
          clearable>
        </el-input>
      </el-col>
      <el-col :span="5">
        <el-button type="primary" plain>查询</el-button>
      </el-col>
    </el-row>
    <el-row :gutter="20">
      <el-col></el-col>
    </el-row>
  </div>
</template>

<script>
  import axios from 'axios'

  export default{
    data() {
      return {
        options2: [{
          value: 'custom_type',
          label: '用户类型'
        },
          {
            value: 'custom_area',
            label: '用户地区',
            disabled: true
          }],
        value2: '',
        input10: ''
      }
    },
    methods: {
      async handleMarket(){
        // 弹框
        this.$alert('<el-button type="primary" plain>查询</el-button>', 'HTML 片段', {
          dangerouslyUseHTMLString: true
        });

        let {data} = await
          axios.get("https://api.myjson.com/bins/13wsgb");
        console.log(data)
      },
      async handleTele() {
      },
      async handleCustomFilter(val) {
        console.log(val);
        console.log(this.value2)
      }
    }
  }
</script>
