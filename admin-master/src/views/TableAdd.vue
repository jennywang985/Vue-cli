<template>
  <div class="HotPot-table-add">
    <el-breadcrumb>
      <el-breadcrumb-item to="/main">Home</el-breadcrumb-item>
      <el-breadcrumb-item>Table management</el-breadcrumb-item>
      <el-breadcrumb-item>Table add</el-breadcrumb-item>
    </el-breadcrumb>
    <br>

    <el-form ref="form" :model="form" label-width="80px">
  <el-form-item label="ID">
    <el-input v-model="form.id"></el-input>
  </el-form-item>
 <el-form-item label="Name">
    <el-input v-model="form.name"></el-input>
  </el-form-item>
   <el-form-item label="Number">
    <el-select v-model="form.region" placeholder="Please select the number range">
      <el-option label="4-6人" value="six"></el-option>
      <el-option label="6-8人" value="eight"></el-option>
      <el-option label="8-10人" value="ten"></el-option>
      <el-option label="10-12人" value="twele"></el-option>
    </el-select>
  </el-form-item>
  <el-form-item label="Table state">
    <el-checkbox-group v-model="form.type">
      <el-checkbox label="Free" name="type"></el-checkbox>
      <el-checkbox label="Reserve" name="type"></el-checkbox>
      <el-checkbox label="Occupy" name="type"></el-checkbox>
      <el-checkbox label="Other" name="type"></el-checkbox>
    </el-checkbox-group>
  </el-form-item>
  
  
  <el-form-item>
    <el-button type="primary" @click="onSubmit">Create now</el-button>
    <el-button>Cancel</el-button>
  </el-form-item>
</el-form>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        form: {
          name: '',
          id:'',
          type: [],
          region: ''   
        }
      }
    },
    methods: {
      onSubmit() {
        console.log('submit!');
      }
    }
  }
</script>