<template>
  <div class="">
    <h1>Add dishes</h1>
    <el-form label-width='100px'>
      <el-form-item label='Dishes pictures: '>
        <el-upload :action="uploadAction" :on-success='doUploadSucc' name="dishImg" :show-file-list='false' class='HotPot-uploader'>
          <img v-if="imageUrl" :src="imageUrl" alt="">
           <i v-else class="el-icon-plus avatar-uploader-icon"></i>
        </el-upload>
      </el-form-item>
    </el-form>
  </div>
</template>
<script>
export default {
  data(){
    return{
      imageUrl:'',  //要显示的预览图片地址
      uploadAction:this.$store.state.globalSettings.apiUrl +'/admin/dish/image', //可处理未见上传的api
      formData:{
        title:'',
        imgUrl:"",
        price:'',            //菜品图片在服务器的文件名称
        detail:'',
        categoryId:''
      }
    }
  },
    methods: {
  doUploadSucc(res,file){
      // 文件上传成功后客户端等到响应消息后的处理函数
      //res:服务端返回的消息
      // file: 从INPUT[type=file]中读取的第一个上传的文件对象
      console.log(res)
      this.form.imgUrl=res.fileName;
      this.imageUrl=URL.createObjectURL(file.raw)
    }
  }
}
</script>

<style lang="scss" >
   .HotPot-uploader {
    .el-upload{
      border:1px dotted #aaa;
      border-radius: 3px;
      cursor: pointer;
      width: 250px;
      height: 177px;
      overflow: hidden;
      &:hover{
       border-color: #409EFF; 
      }
    }
    img{
      max-width:100%;
    }
    .avatar-uploader-icon {
    font-size: 28px;
    color: #8c939d;
    width: 178px;
    height: 178px;
    line-height: 178px;
    text-align: center;
    &:hover{
       color: #409EFF;
    }
  }
  .avatar {
    width: 178px;
    height: 178px;
    display: block;
  }
  }
</style>
