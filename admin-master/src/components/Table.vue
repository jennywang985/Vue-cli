<template>
  <div class="HotPot-table-info">
    <el-card shadow="hover">
      <div class="HotPot-table" :style="{background:getTableColor(data.status)}">{{data.tid}}T: {{data.status | tableStatus}}</div>
      <el-button type="success" plain size="mini" @click="showTableDetail">Details</el-button>
      <el-button type="danger" plain size="mini">Update</el-button>
    </el-card>

    <!-- 桌台详情的对话框 -->
    <el-dialog :title="data.tid+'Table Details'" :visible='dialogTableDetailVisible' :before-close='closeDialogTableDetail'>
      <!-- 对话框主体 -->
      <el-tabs type='border-card' @tab-click='makeQRCode'>
        <el-tab-pane label='Table State'>state loading...</el-tab-pane>
        <el-tab-pane label='Table QR Code'>
          <img :src="qrcodeData" alt="">
        </el-tab-pane>
      </el-tabs>
      <!-- 对话框尾部 -->
      <div slot='footer'>
        <el-button type='primary' @click="dialogTableDetailVisible=false" >Confirm</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<style lang="scss">
.HotPot-table-info {
  padding: 3px;
  text-align: center;

  .HotPot-table {
    width: 90%;
    height: 120px;
    line-height: 120px;
    border: 1px solid #aaa;
    border-radius: 50%;
    box-shadow: 3px -4px 5px #666;
    margin: 5px auto;
  }
}
</style>

<script>
export default {
    data(){
      return{
        dialogTableDetailVisible:false,
        qrcodeData:''  //二维码base64二进制数据
      }
    },
    props:['data'],
    methods:{
      getTableColor(status){
        if(status==1) return '#67C23A';
        else if(status==2) return '#E6A23C';
        else if(status==3) return '#F56C6C';
        else return '#909399'
      },
      showTableDetail(){
        // console.log(this.data) 当前桌子的数据
        this.dialogTableDetailVisible=true;
      },
      closeDialogTableDetail(){
        this.dialogTableDetailVisible=false;
      },
      makeQRCode(){
        //创建二维码--注意此方法不能再当前的mouted中调用,因为绘图必须的canvas在el-dialog中,对话框在组件家再试并不在DOM树上
        var qrcode=require('qrcode');
        // 每个桌子的URL应该形如:
        // http://127.0.0.1:8092/#/3
        var tableUrl=this.$store.state.appUrl+'/#/'+this.data.tid;
        // 把绘制等到的图片二进制数据转换为字符串编码
        qrcode.toDataURL(tableUrl, {
          width:300,
          errorCorrectionLevel:'H'
        }, (err,url)=>{
          this.qrcodeData=url
        })
      }
    }
}
</script>

