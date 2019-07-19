<template>
    <div class="orderHeader">
      <el-row>
        <el-col :span="24">
          <el-breadcrumb separator="/">
            <el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item>
            <el-breadcrumb-item>订单管理</el-breadcrumb-item>
          </el-breadcrumb>
        </el-col>
      </el-row>
      <el-row>
        <el-col :span="6">
          <div class="block">
          <el-date-picker
            v-model="value1"
            align="right"
            type="date"
            placeholder="开始日期"
            :picker-options="pickerOptions1">
          </el-date-picker>
        </div>
        </el-col>
        <el-col :span="16">
        <div class="block">
          <el-date-picker
            v-model="value2"
            align="right"
            type="date"
            placeholder="结束日期"
            :picker-options="pickerOptions1">
          </el-date-picker>
        </div>
        <div class="block block-select">
          <el-dropdown v-model="orderSelect">
            <span class="el-dropdown-link">
            {{orderSelect}}<i class="el-icon-arrow-down el-icon--right"></i>
            </span>
            <el-dropdown-menu slot="dropdown" >
              <el-dropdown-item @click.native="close(i)" v-for="(v,i) in orderSelectOption" :key="i">{{v}}</el-dropdown-item>
            </el-dropdown-menu>
          </el-dropdown>
        </div>
        </el-col>
        <el-col :span="2"></el-col>
      </el-row>
      <el-row>
        <el-col :span="6"><div class="grid-content bg-purple"></div></el-col>
        <el-col :span="5.8">
          <div class="demo-input-suffix">
            <el-input
              placeholder="请输入订单编号"
              prefix-icon="el-icon-search"
              v-model="input">
            </el-input>
          </div>
        </el-col>
        <el-col :span="2"><el-button type="primary" icon="el-icon-search"></el-button></el-col>
      </el-row>
    </div>
</template>
    
<script>
export default {
    name:'orderHeader',
     data() {
      return {
        orderSelect:'订单状态',
        orderSelectOption:['待支付','评价','进行中','待结单','支付超时','已评价'],
        input:'',
        pickerOptions1: {
          disabledDate(time) {
            return time.getTime() > Date.now();
          },
          shortcuts: [{
            text: '今天',
            onClick(picker) {
              picker.$emit('pick', new Date());
            }
          }, {
            text: '昨天',
            onClick(picker) {
              const date = new Date();
              date.setTime(date.getTime() - 3600 * 1000 * 24);
              picker.$emit('pick', date);
            }
          }, {
            text: '一周前',
            onClick(picker) {
              const date = new Date();
              date.setTime(date.getTime() - 3600 * 1000 * 24 * 7);
              picker.$emit('pick', date);
            }
          }]
        },
        value1: '',
        value2: '',
      };
    },
    methods:{
      close(index){
        this.orderSelect = this.orderSelectOption[index];
      }
    }
  };

</script>

<style lang="less">
.orderHeader{
  margin: 30px 50px 10px;
  .el-row{
    margin-bottom: 15px;
    .block{
    float: left
    }
    .block-select{
      margin-left: 50px;
      line-height: 37px;
      border: 1px solid #DCDFE6;
      border-radius: 4px;
      width: 150px;
    }
    .bg-purple{
      background: white;
    }
  }
}
</style>


