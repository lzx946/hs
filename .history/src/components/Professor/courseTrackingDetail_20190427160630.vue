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
            <div style="font-size:18px">
                <p class="title">北京大学xxx教授</p>
                <p><span style="margin-right: 30px;">开课时间：2018年01月01号</span><span>开课时间：2018年01月01号</span></p>
                <p>课程地点及具体时间</p>
                <div class="areaBox">
                    <div class="area" v-for="(item,index) in areas" :key="index">
                        <p><span style="font-weight:bold">{{item.name}}</span>：{{item.detail}}</p>
                        <p>{{item.date}}</p>
                    </div>
                </div>
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
            }],
            areas: [{
                name: '罗马',
                detail: '罗马XXXXXX酒店XXXXXXXXX房间号XXXXXXXXX',
                date: '2018年01月01日'
            },{
                name: '米兰',
                detail: '米兰XXXXXX酒店XXXXXXXXX房间号XXXXXXXXX',
                date: '2018年01月01日'
            },{
                name: '希腊',
                detail: '希腊XXXXXX酒店XXXXXXXXX房间号XXXXXXXXX',
                date: '2018年01月01日'
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
        padding: 15px 100px; 
    }
    .title {
        font-size: 25px;

    }
    .subtitle {
        font-size: 15px;
    }
    .areaBox {
        display: flex;
        width: auto;
    }
    .area {
        flex: 0 0 30%;
        padding-right: 10px;
        border-top: 3px solid #19568a;
    }
</style>

