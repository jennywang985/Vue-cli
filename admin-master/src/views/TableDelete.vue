<template>
   <div class="HotPot-table-delete">
    <el-breadcrumb>
      <el-breadcrumb-item to="/main">Home</el-breadcrumb-item>
      <el-breadcrumb-item>Table management</el-breadcrumb-item>
      <el-breadcrumb-item>Table deletion</el-breadcrumb-item>
    </el-breadcrumb>
    <br>
    <el-form :model="numberValidateForm" ref="numberValidateForm" label-width="100px" class="demo-ruleForm">
  <el-form-item
    label="Table ID"
    prop="age"
    :rules="[
      { required: true, message: 'ID cannot be empty'},
      { type: 'number', message: 'ID must be a numeric value'}
    ]">
    <el-input type="age" v-model.number="numberValidateForm.age" autocomplete="off"></el-input>
  </el-form-item>
  <el-form-item>
    <el-button type="primary" @click="submitForm('numberValidateForm')">Submit</el-button>
    <el-button @click="resetForm('numberValidateForm')">Reset</el-button>
  </el-form-item>
</el-form>
   </div>
</template>
<script>
  export default {
    data() {
      return {
        numberValidateForm: {
          age: ''
        }
      };
    },
    methods: {
      submitForm(formName) {
        this.$refs[formName].validate((valid) => {
          if (valid) {
            alert('submit!');
          } else {
            console.log('error submit!!');
            return false;
          }
        });
      },
      resetForm(formName) {
        this.$refs[formName].resetFields();
      }
    }
  }
</script>