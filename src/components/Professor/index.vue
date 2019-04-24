<template>
    <div :style="`margin-top:80px;height:${heightBrower-80}px`">
        <el-tabs v-model="activeName" type="card" >
    <el-tab-pane label="用户管理" name="first">用户管理</el-tab-pane>
    <el-tab-pane label="配置管理" name="second">配置管理</el-tab-pane>
    <el-tab-pane label="角色管理" name="third">角色管理</el-tab-pane>
    <el-tab-pane label="定时任务补偿" name="fourth">定时任务补偿</el-tab-pane>
  </el-tabs>
  <el-steps :active="active" finish-status="success">
    <el-step title="步骤 1"></el-step>
    <el-step title="步骤 2"></el-step>
    <el-step title="步骤 3"></el-step>
</el-steps>

<el-button type="primary">但是</el-button>
    </div>
</template>
<script>
import { common } from '@/util/common.js'
export default {
    data() {
      return {
           active: 0,
          activeName: 'first',
        heightBrower: common.heightBrower,
      };
    },
    methods: {
      
    }
}
</script>
<style scoped>

</style>

