<template>
  <div class="OrderList">
    <el-breadcrumb>
      <el-breadcrumb-item to="/main">Home</el-breadcrumb-item>
      <el-breadcrumb-item>Order management</el-breadcrumb-item>
      <el-breadcrumb-item>Order list</el-breadcrumb-item>
    </el-breadcrumb>
    <br>
  <el-table :data="tableData" border style="width: 100%">
    <el-table-column prop="date" label="Order number"  width="180"> </el-table-column>
    <el-table-column  prop="name" label="start time"  width="180"> </el-table-column>
    <el-table-column prop="address"  label="end time"> </el-table-column>
    <el-table-column prop="address"  label="Number of diners"> </el-table-column>
    <el-table-column prop="address"  label="Table number"> </el-table-column>
    <el-table-column prop="address"  label="Menu details"> </el-table-column>
  </el-table>
  </div>
</template>
