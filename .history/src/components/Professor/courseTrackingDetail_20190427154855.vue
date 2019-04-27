<template>
    <div :style="`height:${heightBrower-80}px; width:80%; max-width:1400px;margin:0 auto;margin-top:50px;`">    
        <el-steps :active="active" finish-status="success">
            <el-step :title="item.title" :description="item.description" v-for="item in progress" :key="item.title"></el-step>
        </el-steps>

        <div class="courseContainer">
            <img src="@/assets/logo.png" style="width:250px;height:360px;float: left;">
            <div class="titleBox">
                <p class="title">“组织管理智慧”</p>
                <p class="subtitle">欧洲华商学院 第16期</p>
            </div>
        </div>
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

    .titleBox {
        background: #19568a;
        margin-left: 250px;
        padding-left: 100px;
    }
    .title {
        font-size: 30px;

    }
    .subtitle {
        font-size: 18px;
    }
</style>

