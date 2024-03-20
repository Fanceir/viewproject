<template>
  <div class="modify-admin-info-page">
    <div class="admin-info-header">
      <h1 class="page-title">修改管理员信息</h1>
      <p class="sub-title">在下方填写新的管理员信息和密码</p>
    </div>
    <el-form :model="adminInfo" label-width="120px" class="admin-info-form" ref="adminForm">
      <el-form-item label="用户名">
        <el-input v-model="adminInfo.username" disabled />
      </el-form-item>
      <el-form-item label="姓名">
        <el-input v-model="adminInfo.name" placeholder="请输入管理员姓名" />
      </el-form-item>
      <el-form-item label="邮箱">
        <el-input v-model="adminInfo.email" placeholder="请输入管理员邮箱" />
      </el-form-item>
      <el-form-item label="新密码">
        <el-input v-model="adminInfo.newPassword" type="password" placeholder="请输入新密码" />
      </el-form-item>
      <el-form-item label="确认密码">
        <el-input v-model="adminInfo.confirmPassword" type="password" placeholder="请再次输入新密码" />
      </el-form-item>
      <el-form-item class="form-buttons">
        <el-button type="primary" @click="submitForm">保存修改</el-button>
        <el-button @click="cancelForm">取消</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      adminInfo: {
        username: 'admin', // 您可以使用实际数据填充此字段
        name: '',
        email: '',
        newPassword: '',
        confirmPassword: ''
      }
    }
  },
  methods: {
    submitForm() {
      // 检查必填字段是否为空
      if (!this.adminInfo.name || !this.adminInfo.email || !this.adminInfo.newPassword || !this.adminInfo.confirmPassword) {
        this.$message.error('所有信息均不能为空！')
        return
      }
      // 检查密码是否匹配
      if (this.adminInfo.newPassword !== this.adminInfo.confirmPassword) {
        // 处理密码不匹配错误
        this.$message.error('确认密码与新密码不一致！')
        return
      }
      // 提交表单和更新管理员信息的逻辑
      // 更新成功后显示成功消息
      this.$message.success('修改成功！')
      setTimeout(() => {
        // 隐藏成功消息
        this.$message.closeAll()
      }, 3000)// 3秒后隐藏消息
    },
    cancelForm() {
      // 清空表单数据
      this.$refs.adminForm.resetFields()
    }
  }
}
</script>

<style scoped>
.modify-admin-info-page {
  max-width: 600px;
  margin: 0 auto;
}

.admin-info-header {
  text-align: center;
  margin-bottom: 30px;
}

.page-title {
  font-size: 24px;
  margin-bottom: 5px;
}

.sub-title {
  color: #666;
  font-size: 14px;
}

.admin-info-form {
  background-color: #f7f7f7;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
}

.form-buttons {
  text-align: center;
  margin-top: 30px;
}
</style>
