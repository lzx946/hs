<template>
    <div :style="`margin-top:80px;height:${heightBrower-80}px`">    
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

