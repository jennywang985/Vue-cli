<template>
  <div class="login">
    <el-card class="HotPot-login-card">
      <div slot="header">Administrator login</div>
      <div>
        <el-form label-width="100px">

          <el-form-item label="Administrator：">
            <el-input v-model="formData.aname" placeholder="Please enter the administrator name"></el-input>
          </el-form-item>
        
          <el-form-item label="password：">
            <el-input type="password" v-model="formData.apwd" placeholder="Please enter the administrator password"></el-input>
          </el-form-item>

          <el-form-item>
            <el-button type="primary" @click="doLogin">Sign in</el-button>
            <el-button @click="doCancel">Cancel</el-button>
          </el-form-item>
        
        </el-form>
      </div>
    </el-card>
  </div>
</template>

<script>
export default {
  data(){   //普通组件的模型数据是函数返回值
    return {
      formData: { //表单中用户输入的两个数据
        aname: 'admin',
        apwd: '123456'
      }
    }
  },
  methods:{
    doLogin(){  //执行登录
      var url = this.$store.state.globalSettings.apiUrl+`/admin/login/${this.formData.aname}/${this.formData.apwd}`;

      this.$axios.get(url).then((res)=>{
        if(res.data.code==200){ //登录成功
          //把用户名存入Vuex存储仓库
          this.$store.commit('setAdminName',this.formData.aname);
          //执行视图跳转
          this.$router.push('/main');
        }else { //登录失败
          this.$alert('Error in username or password！','Login failed',{type:'error'}).then(()=>{}).catch(()=>{});
        }
      }).catch((err)=>{
        console.log(err);
      })
    },
    doCancel(){ //清除用户的输入
      this.formData.aname = '';
      this.formData.apwd = '';
    }
  }
}  
</script>

<style lang="scss">
  .HotPot-login-card {
    width: 450px;
    margin: 100px auto;

    .el-card__header {
      text-align: center;
      font-size: 1.2em;
    }
  }
</style>
