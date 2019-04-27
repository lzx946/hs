<template>
    <div :style="`height:${heightBrower-80}px; width:80%; max-width:1400px;margin:0 auto;margin-top:80px;`">    
        <el-steps :active="active" finish-status="success">
            <el-step :title="item.title" :description="item.description" v-for="item in progress" :key="item.title"></el-step>
        </el-steps>
    </div>
</template>
<script>
import { common } from '@/util/common.js'
export default {
    data() {
        return {
            heightBrower: common.heightBrower,
            active: 2,
            progress:[{
                title: '申请课程',
                description: '时间*******'
            },{
                title: '审核',
                description: '时间*******'
            },{
                title: '材料上传',
                description: '时间*******'
            },{
                title: '开课',
                description: '时间*******'
            },{
                title: '结课',
                description: '时间*******'
            }]
        };
    },
    methods: {
      
    }
}
</script>
<style scoped>

</style>

