<template>
  <div class="settings">
    <el-breadcrumb>
      <el-breadcrumb-item to="/main">Home</el-breadcrumb-item>
      <el-breadcrumb-item>Global Settings</el-breadcrumb-item>
    </el-breadcrumb>

    <br>
    <el-card shadow="never">
      <el-form label-width="110px" >
      
        <el-form-item label="Apply Name：">
          <el-input v-model="formData.appName"></el-input>
        </el-form-item>

        <el-form-item label="API Address：">
          <el-input v-model="formData.apiUrl"></el-input>
        </el-form-item>

        <el-form-item label="ManageAddress：">
          <el-input v-model="formData.adminUrl"></el-input>
        </el-form-item>

        <el-form-item label="CustomerAddress：">
          <el-input v-model="formData.appUrl"></el-input>
        </el-form-item>

        <el-form-item label="ICP record：">
          <el-input v-model="formData.icp"></el-input>
        </el-form-item>

        <el-form-item label="Copyright：">
          <el-input v-model="formData.copyright"></el-input>
        </el-form-item>

        <el-form-item>
          <el-button type="primary" @click="doSubmot">Submit</el-button>
          <el-button @click="doCancel">Cancel</el-button>
        </el-form-item>
      </el-form>
    </el-card>
  </div>
</template>

<script>
export default {
  data(){
    return {
      formData:{
        appName:'',
        apiUrl:'',
        appUrl:'',
        adminUrl:'',
        icp:'',
        copyright:'',
       }
    }
  },
  mounted(){
    //将$store存储中的全局配置数据赋值给中间变量-formData，方便表单元素执行双向数据绑定
    // 引用复制,两个变量指向一个对象
    // this.formData = this.$store.state.globalSettings;
    // 对象复制,创建出两个一样的对象
    this.formData.appName=this.$store.state.globalSettings.appName;
    this.formData.appUrl=this.$store.state.globalSettings.appUrl;
    this.formData.adminUrl=this.$store.state.globalSettings.adminUrl;
    this.formData.apiUrl=this.$store.state.globalSettings.apiUrl;
    this.formData.icp=this.$store.state.globalSettings.icp;
    this.formData.copyright=this.$store.state.globalSettings.copyright;
  },
  methods:{
    doSubmot(){
      var url=this.$store.state.globalSettings.apiUrl+'/admin/settings';
     
      this.$axios.put(url,this.formData).then((res)=>{
        if(res.data.code==200){
          this.$message.success('Successful modification of global settings!');
          // TODO:修改$store中的全局设置
        }else{
          this.$message.error('Global Settings Modification Failed!')
        }
      }).catch((err)=>{
        console.log(err);
      })
    },
    doCancel(){
      this.formData.appName=this.$store.state.globalSettings.appName;
      this.formData.appUrl=this.$store.state.globalSettings.appUrl;
      this.formData.adminUrl=this.$store.state.globalSettings.adminUrl;
      this.formData.apiUrl=this.$store.state.globalSettings.apiUrl;
      this.formData.icp=this.$store.state.globalSettings.icp;
      this.formData.copyright=this.$store.state.globalSettings.copyright;
    }
  }
}
</script>
