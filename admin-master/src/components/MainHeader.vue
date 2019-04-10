<template>
  <div class="HotPot-main-header">
    <h3 class="HotPot-title">{{$store.state.globalSettings.appName}}Admin Dashboard</h3>
    <div class="HotPot-right">
      Current User：{{$store.state.adminName}}
      <el-button size="mini" @click="quit">quit</el-button>
    </div>
  </div>
</template>

<script>
export default {
  methods:{
    quit(){
      //清除当前用户的登录信息
      this.$store.commit('setAdminName', '');
      //跳转回登录页
      this.$router.push('/login');
    }
  }
}
</script>

<style lang="scss">
$header-height: 60px;

.HotPot-main-header {
  background: #DCDFE6;
  border-radius: 4px;
  line-height: $header-height;
  height: $header-height;
  padding: 0 6px;

  .HotPot-title {
    color: #303133;
    float: left;
    margin: 0;
  }
  .HotPot-right {
    float:right;
  }
}
</style>