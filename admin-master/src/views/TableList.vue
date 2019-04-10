<template>
  <div class="HotPot-table-list">
    <el-breadcrumb>
      <el-breadcrumb-item to="/main">Home</el-breadcrumb-item>
      <el-breadcrumb-item>Table management</el-breadcrumb-item>
      <el-breadcrumb-item>Table list</el-breadcrumb-item>
    </el-breadcrumb>
    <br>
    <el-row>
      <el-col v-for="(t,i) in tableList" :key='(t.index,i.index)' :xs="12" :sm="8" :md="6" :lg="4" :xl="2" :span="24">
        <HotPot-table :data="t"></HotPot-table>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import Table from '../components/Table'
export default {
  data(){
    return{
      tableList:[]
    }
  },
  mounted(){
    //加载桌台列表
    var url=this.$store.state.globalSettings.apiUrl + '/admin/table';
    this.$axios.get(url).then(({data})=>{
      this.tableList=data;
    }).catch((err)=>{
      console.log(err)
    })
  },
  components:{
    'HotPot-table':Table
  }
}
</script>
