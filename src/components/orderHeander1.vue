<template>
    <div>
        <el-breadcrumb separator="/">
            <el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item>
            <el-breadcrumb-item>订单管理</el-breadcrumb-item>
        </el-breadcrumb>
        
        <button @click="exportExcel">weqe</button>
        <tr>
            <td></td>
            <td></td>
            <td></td>
        </tr>
    </div>
</template>
    
<script>
export default {
    name:'Crumbs',
    data () {
    return {
      tableData: [
        {'index':'0',"nickName": "沙滩搁浅我们的旧时光", "name": "小明"},
        {'index':'1',"nickName": "女人天生高贵", "name": "小红"},
        {'index':'2',"nickName": "海是彩色的灰尘", "name": "小兰"}
      ]
    }
  },
    methods:{
        exportExcel() {
        require.ensure([], () => {
          const { export_json_to_excel } = require('../vendor/Export2Excel.js');
          const tHeader = ['序号', '昵称', '姓名'];
          // 上面设置Excel的表格第一行的标题
          const filterVal = ['index', 'nickName', 'name'];
          // 上面的index、nickName、name是tableData里对象的属性
          const list = this.tableData;  //把data里的tableData存到list
          const data = this.formatJson(filterVal, list);
          export_json_to_excel(tHeader, data, '列表excel');
        })
      },
      formatJson(filterVal, jsonData) {
        return jsonData.map(v => filterVal.map(j => v[j]))
      }

    }
}
</script>

<style lang="less">

</style>


