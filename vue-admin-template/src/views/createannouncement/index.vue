<!--
 * @Author: fanc1
 * @Date: 2024-03-19 20:53:38
 * @LastEditors: fanc1
 * @LastEditTime: 2024-03-20 19:20:11
 -->
<template>
  <div class="create-announcement-page">
    <h1 class="page-title">创建公告</h1>
    <el-form :model="form" label-width="80px" class="announcement-form">
      <el-form-item label="标题">
        <el-input v-model="form.title" placeholder="请输入公告标题" />
      </el-form-item>
      <el-form-item label="内容">
        <el-input type="textarea" v-model="form.content" placeholder="请输入公告内容" />
      </el-form-item>
      <el-form-item class="form-buttons">
        <el-button type="primary" @click="submitForm">发布</el-button>
        <el-button @click="cancelForm">取消</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<style scoped>
.create-announcement-page {
  max-width: 600px;
  margin: 0 auto;
}

.page-title {
  text-align: center;
  margin-bottom: 20px;
}

.announcement-form {
  background-color: #f7f7f7;
  padding: 20px;
  border-radius: 8px;
}

.form-buttons {
  text-align: center;
  margin-top: 20px;
}
</style>

<script>
export default {
  data() {
    return {
      form: {
        title: '',
        content: ''
      }
    }
  },
  methods: {
    submitForm() {
      // 在这里发送公告数据到后端保存的逻辑
      // 省略...
      // 发送成功后可以跳转到公告列表页面或者给出提示
      this.$message('提交')
      // 示例：跳转到公告列表页
      this.$router.push('/announcement/index')
    },
    cancelForm() {
      // 取消发布，清空表单数据
      this.form.title = ''
      this.form.content = ''
    }
  }
}
</script>

<style scoped>
.create-announcement-page {
  max-width: 600px;
  margin: auto;
}

.el-form-item__label {
  font-weight: bold;
}
</style>
