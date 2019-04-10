<template>
  <div class="">
    <h1>List of dishes</h1>
    <el-tabs type='border-card'>
      <el-tab-pane v-for="(c,i) in dishList"  :key="(c.index,i.index)">
        <span slot='label' >
          <el-badge :value="c.dishList.length" class="item">{{c.cname}}</el-badge>
        </span>
        <el-row>
          <el-col v-for="(d,j) in c.dishList" :key="(d.index,j.index)" :xs="12" :md="6" :lg="4" :xl='3' style="padding:10px">
            <!-- <HotPot-dis h :data='d'></HotPot-dish> -->
            <img :src="require('../assets/img/dish/'+d.imgUrl)"  alt="" style='max-width:100%'>
            {{d.title}}
            {{d.price}}.00
          </el-col>
        </el-row>
      </el-tab-pane>
    </el-tabs>
  </div>
</template>

<script>
export default {
  data(){
    return {
      dishList:[]
   }
  },
  mounted(){
    // 异步获取菜品
    var url=this.$store.state.globalSettings.apiUrl + '/admin/dish'
    this.$axios.get(url).then(({data})=>{
      this.dishList=data;
    }).catch((err)=>{
      console.log(err)
    })
  }
}
</script>
<style lang="scss">
  .item {
      margin-top: 7px;
      margin-right: 40px;
      border-radius: 30%;
      padding-bottom: 10px;
}

</style>
