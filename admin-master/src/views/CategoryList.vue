<template>
  <div class="HotPot-category">
    <el-breadcrumb>
      <el-breadcrumb-item to="/main">Home</el-breadcrumb-item>
      <el-breadcrumb-item>Category Management of Dishes</el-breadcrumb-item>
      <el-breadcrumb-item>Category list</el-breadcrumb-item>
    </el-breadcrumb>
   <br>
    <el-button type='primary' @click="addCategory">Add a new category of dishes</el-button>
  <br>
    <el-table :data='categoryList'  stripe border>
         <el-table-column label='ID' prop='cid'> </el-table-column>
         <el-table-column label='Name' prop='cname'> </el-table-column>
         <el-table-column label='operation' > 
           <template slot-scope="{row,$index}">
              <el-button @click='updateCategory(row,$index)' type='success' size='mini'>Update</el-button>
              <el-button @click="deleteCategory(row,$index)" type='danger' size='mini'>Delete</el-button>
           </template>
         </el-table-column>
    </el-table>
  </div>
</template>

<script>
export default {
  data(){
    return {
      categoryList:[]
    }
  },
  methods:{
    deleteCategory(c,i){
      this.$confirm('Delete operation is irrevocable! Are you sure?','Prompt',{type:'warning'}).then(()=>{
         var url=this.$store.state.globalSettings.apiUrl + '/admin/category/'+c.cid;
          this.$axios.delete(url).then((res)=>{
        if(res.data.code==200){//数据库删除成功
          this.categoryList.splice(i, 1);  //从模型数据中删除
          this.$message.success('Successful Deletion of Categories!');
        }else{
          this.$message.error('Category deletion error:'+res.data.msg);
        }
      }).catch((err)=>{
        console.log(err);
      })
      }).catch(()=>{

      })
    },
    updateCategory(c,i) {
      console.log(i);
    },
    addCategory(){
      this.$prompt('Please enter a new category name:','Prompt',{type:'info'}).then(({value})=>{
        //获得用户的输入,调用数据API添加到数据库
        var url=this.$store.state.globalSettings.apiUrl + '/admin/category';
        this.$axios.post(url,{cname:value}).then((res)=>{
          if(res.data.code==200){
            //数据库中添加成功
            this.$message.success('New Category Added Successfully')
            //模型数据中添加新的类别
            this.categoryList.push({cid:res.data.cid,cname:value})
          }else{
            this.$message.error('New Category Add Error: '+res.data.msg)
          }
        }).catch((err)=>{
          console.log(err)
        })
      }).catch(()=>{

      })
    }
  },
  mounted(){
    var url=this.$store.state.globalSettings.apiUrl + '/admin/category';
    this.$axios.get(url).then((res)=>{
      this.categoryList=res.data;
    }).catch((err)=>{
      console.log(err);
    })
  } 
}
</script>