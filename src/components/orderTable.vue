<template>
    <div class="orderTable">
      <el-tabs v-model="activeName" @tab-click="handleClick">
        <el-tab-pane label="订单明细" name="first">
        <el-row>
          <el-col :span="2.5"><el-button type="warning">批量删除</el-button></el-col>
          <el-col :span="8"><div class="grid-content bg-purple"></div></el-col>
          <el-col :span="8"><div class="grid-content bg-purple"></div></el-col>
        </el-row>
        <el-table
            ref="multipleTable"
            :data="tableData3"
            tooltip-effect="dark"
            style="width: 100%"
            @selection-change="handleSelectionChange">
            <el-table-column
                type="selection"
                width="55">
            </el-table-column>
            <el-table-column
                prop="name"
                label="订单编号"
                width="150">
            </el-table-column>
            <el-table-column
                label="下单日期"
                width="110">
            <template slot-scope="scope">{{ scope.row.date }}</template>
            </el-table-column>
            <el-table-column
                label="结束日期"
                width="110">
            <template slot-scope="scope">{{ scope.row.date }}</template>
            </el-table-column>
            <el-table-column
                prop="name"
                label="陪玩名称"
                width="90">
            </el-table-column>
            <el-table-column
                prop="name"
                label="客户名称"
                width="90">
            </el-table-column>
            <el-table-column
                prop="address"
                label="订单金额"
                width="90">
            </el-table-column>
            <el-table-column
                prop="address"
                label="订单状态"
                width="90">
            </el-table-column>
            <el-table-column
                prop="address"
                label="操作"
                show-overflow-tooltip>
                <i class="el-icon-tickets orderIco" @click="dialogVisible1 = true"></i>
                <i class="el-icon-edit orderIco" @click="dialogVisible2 = true"></i>
                <i class="el-icon-delete orderIco" @click="orderDelete"></i>
            </el-table-column>
        </el-table>
        <el-dialog
          title="查看订单"
          :visible.sync="dialogVisible1"
          width="65%">
          <el-row>
            <el-col :span="3">订单编号:</el-col>
            <el-col :span="7"><span>1</span></el-col>
            <el-col :span="1"><div class="grid-content bg-purple"></div></el-col>
            <el-col :span="3">游戏类型:</el-col>
            <el-col :span="7"><span></span></el-col>
          </el-row>
          <el-row>
            <el-col :span="3">下单日期:</el-col>
            <el-col :span="7"><span>1</span></el-col>
            <el-col :span="1"><div class="grid-content bg-purple"></div></el-col>
            <el-col :span="3">结束日期:</el-col>
            <el-col :span="7"><span>1</span></el-col>
          </el-row>
          <el-row>
            <el-col :span="3">陪玩名称:</el-col>
            <el-col :span="7"><span>1</span></el-col>
            <el-col :span="1"><div class="grid-content bg-purple"></div></el-col>
            <el-col :span="3">客户名称:</el-col>
            <el-col :span="7"><span></span></el-col>
          </el-row>
          <el-row>
            <el-col :span="3">订单金额:</el-col>
            <el-col :span="7"><span>1</span></el-col>
            <el-col :span="1"><div class="grid-content bg-purple"></div></el-col>
            <el-col :span="3">订单状态:</el-col>
            <el-col :span="7"><span></span></el-col>
          </el-row>
          <div class="orderButton">
              <el-row>
                <el-col :span="9"><div class="grid-content bg-purple"></div></el-col>
                <el-col :span="3"><el-button @click="dialogVisible1 = false">取消</el-button></el-col>
                <el-col :span="2"><el-button type="primary" @click="dialogVisible1 = false">确定</el-button></el-col>
                <el-col :span="8"><div class="grid-content bg-purple"></div></el-col>
              </el-row>
          </div>
        </el-dialog>
          <el-dialog
          title="修改订单"
          :visible.sync="dialogVisible2"
          width="65%">
          <el-row>
            <el-col :span="3">订单编号:</el-col>
            <el-col :span="7"><span>1</span></el-col>
            <el-col :span="1"><div class="grid-content bg-purple"></div></el-col>
            <el-col :span="3">游戏类型:</el-col>
            <el-col :span="7"><span></span></el-col>
          </el-row>
          <el-row>
            <el-col :span="3">下单日期:</el-col>
            <el-col :span="7"><el-input v-model="input"></el-input></el-col>
            <el-col :span="1"><div class="grid-content bg-purple"></div></el-col>
            <el-col :span="3">结束日期:</el-col>
            <el-col :span="7"><el-input v-model="input"></el-input></el-col>
          </el-row>
          <el-row>
            <el-col :span="3">陪玩名称:</el-col>
            <el-col :span="7"><el-input v-model="input"></el-input></el-col>
            <el-col :span="1"><div class="grid-content bg-purple"></div></el-col>
            <el-col :span="3">客户名称:</el-col>
            <el-col :span="7"><el-input v-model="input"></el-input></el-col>
          </el-row>
          <el-row>
            <el-col :span="3">订单金额:</el-col>
            <el-col :span="7"><el-input v-model="input"></el-input></el-col>
            <el-col :span="1"><div class="grid-content bg-purple"></div></el-col>
            <el-col :span="3">订单状态:</el-col>
            <el-col :span="7"><el-input v-model="input"></el-input></el-col>
          </el-row>
          <div class="orderButton">
              <el-row>
                <el-col :span="9"><div class="grid-content bg-purple"></div></el-col>
                <el-col :span="3"><el-button @click="orderClose1">取消</el-button></el-col>
                <el-col :span="2"><el-button type="primary" @click="orderClose2">确定</el-button></el-col>
                <el-col :span="8"><div class="grid-content bg-purple"></div></el-col>
              </el-row>
          </div>
        </el-dialog>
        <div class="orderFoot">
          <el-row>
            <el-col :span="2.5"><el-button type="success">导出Excel</el-button></el-col>
            <el-col :span="15">
              <div class="block">
                <el-pagination
                @size-change="handleSizeChange"
                @current-change="handleCurrentChange"
                :current-page.sync="currentPage3"
                :page-size="100"
                layout="prev, pager, next, jumper"
                :total="1000"
                background>
                </el-pagination>
              </div>
            </el-col>
            <el-col :span="2"><div class="grid-content bg-purple"></div></el-col>
          </el-row>
        </div>
        </el-tab-pane>
        <el-tab-pane label="图表" name="second">
          <div id="main" style="width:1000px;height:500px"></div>
        </el-tab-pane>
      </el-tabs>
    </div>
</template>

<script>
import echarts from 'echarts'
export default {
    name:'orderTable',
    data() {
      return {
        currentPage1: 5,
        currentPage2: 5,
        currentPage3: 5,
        currentPage4: 4,
        activeName: 'first',
        dialogVisible1: false,
        dialogVisible2: false,
        tableData3: [{
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市'
        }, {
          date: '2016-05-02',
          name: '王小虎',
          address: '上海市'
        }, {
          date: '2016-05-04',
          name: '王小虎',
          address: '上海市'
        }, {
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市'
        }, {
          date: '2016-05-08',
          name: '王小虎',
          address: '上海市'
        }],
        multipleSelection: []
      }
    },

    methods: {
      drawChart(){
          let option={
            tooltip : {
                trigger: 'item',
                formatter: "{a} <br/>{b} : {c} ({d}%)"
            },
            legend: {
                orient: 'vertical',
                left: 'left',
                data: ['直接访问','邮件营销','联盟广告','视频广告','搜索引擎']
            },
            series : [
                {
                    name: '访问来源',
                    type: 'pie',
                    radius : '55%',
                    center: ['50%', '60%'],
                    data:[
                        {value:335, name:'直接访问'},
                        {value:310, name:'邮件营销'},
                        {value:234, name:'联盟广告'},
                        {value:135, name:'视频广告'},
                        {value:1548, name:'搜索引擎'}
                    ],
                    itemStyle: {
                        emphasis: {
                            shadowBlur: 10,
                            shadowOffsetX: 0,
                            shadowColor: 'rgba(0, 0, 0, 0.5)'
                        }
                    }
                }
            ]
          }
        this.myChart.setOption(option);
        window.onresize=function(){
        this.myChart.resize()
      }
      },
      handleSizeChange(val) {
        console.log(`每页 ${val} 条`);
      },
      handleCurrentChange(val) {
        console.log(`当前页: ${val}`);
      },
      handleClick(tab, event) {
        console.log(tab, event);
      },
      toggleSelection(rows) {
        if (rows) {
          rows.forEach(row => {
            this.$refs.multipleTable.toggleRowSelection(row);
          });
        } else {
          this.$refs.multipleTable.clearSelection();
        }
      },
      handleSelectionChange(val) {
        this.multipleSelection = val;
      },
      orderClose1() {
        this.dialogVisible2=false;
        this.$message({
          type: 'info',
          message: '取消修改!'
        })
        },
        // this.$confirm('此操作将永久删除该文件, 是否继续?', '提示', {
        //   confirmButtonText: '确定',
        //   cancelButtonText: '取消',
        //   type: 'warning'
        // }).then(() => {
        //   ;
        // }).catch(() => {
        //   this.$message({
        //     type: 'info',
        //     message: '已取消删除'
        //   });          
        // });
        orderClose2() {
        this.dialogVisible2=false;
        this.$message({
          type: 'success',
          message: '修改成功!'
        })
        },
      orderDelete() {
        this.$confirm('此操作将永久删除该订单, 是否继续?', '提示', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          type: 'warning'
        }).then(() => {
          this.$message({
            type: 'success',
            message: '删除成功!'
          });
        }).catch(() => {
          this.$message({
            type: 'info',
            message: '已取消删除'
          });          
        });
      }
    },
    mounted(){
       this.myChart=this.$echarts.init(document.getElementById('main'));
       this.drawChart();
    },
    
  }
</script>

<style lang="less">
  .orderTable{
    margin: 0 50px 20px;
    .orderIco{
      margin-left: 20px
    }
    .has-gutter{
      .el-table_1_column_9{
        .cell{
          text-indent: 41px
        }
      }
    }
    .bg-purple{
      background: white
    }
    .el-dialog__wrapper .el-dialog__body .el-col-3{
      line-height: 38px
    }
    .el-dialog__wrapper .el-dialog__body .el-row{
      margin-top: 10px
    }
    .el-dialog__wrapper .el-dialog__body .orderButton{
      margin-top: 50px
    }
    .orderFoot{
    margin: 20px 0;
  .el-row{
    .bg-purple{
      background: white;
    }
  }
    }
  }
  
</style>

