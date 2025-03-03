<template>
    <div>
      <el-button type="primary" @click="handleClick">点击我</el-button>
      <el-input v-model="message" placeholder="请输入内容"></el-input>
      <p>输入内容：{{ message }}</p>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        message: ''
      }
    },
    methods: {
      handleClick() {
        this.$message.success('按钮被点击了！')
      }
    }
  }
  </script>
  