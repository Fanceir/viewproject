<!--
 * @Author: fanc1
 * @Date: 2024-03-19 20:53:38
 * @LastEditors: fanc1
 * @LastEditTime: 2024-03-20 19:09:11
 -->
<template>
  <div class="app-container">
    <el-form ref="form" :model="form" label-width="120px">
      <el-form-item label="活动名称">
        <el-input v-model="form.name" placeholder="请输入活动名称" />
      </el-form-item>
      <el-form-item label="活动地区">
        <el-input v-model="form.region" placeholder="请输入活动的地区" />
      </el-form-item>
      <el-form-item label="活动所属学院">
        <el-input v-model="form.college" placeholder="请输入所属学院" />
      </el-form-item>
      <el-form-item label="活动时间">
        <el-col :span="11">
          <el-date-picker v-model="form.date1" type="date" placeholder="活动举行的日期" style="width: 100%;" />
        </el-col>
        <el-col :span="2" class="line">-</el-col>
        <el-col :span="11">
          <el-time-picker v-model="form.date2" type="fixed-time" placeholder="选择一个具体的时间" style="width: 100%;" />
        </el-col>
      </el-form-item>
      <el-form-item label="活动的种类">
        <el-checkbox-group v-model="form.type">
          <el-checkbox label="线上活动" name="type" />
          <el-checkbox label="推广活动" name="type" />
          <el-checkbox label="线下活动" name="type" />
          <el-checkbox label="简单品牌曝光" name="type" />
          <el-checkbox label="其他" name="type" />
        </el-checkbox-group>
      </el-form-item>
      <el-form-item label="赞助商">
        <el-radio-group v-model="form.resource">
          <el-radio label="有赞助商" />
          <el-radio label="无赞助商" />
        </el-radio-group>
      </el-form-item>
      <el-form-item label="活动描述">
        <el-input v-model="form.desc" type="textarea" placeholder="请输入活动描述" />
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="onSubmit">创建</el-button>
        <el-button @click="onCancel">取消</el-button>
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
        region: '',
        college: '',
        date1: '',
        date2: '',
        type: [],
        resource: '',
        desc: ''
      }
    }
  },
  methods: {
    onSubmit() {
      this.$message('提交')
    },
    onCancel() {
      this.$message({
        message: '取消创建活动',
        type: 'warning'
      })
    }
  }
}
</script>
