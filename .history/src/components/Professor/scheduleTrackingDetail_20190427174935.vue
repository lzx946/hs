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
        
        <div class="inviteContainer">
            <p  style="clear:both;">
                <span class="minorTitle">接受邀请（课程具体地点和时间）</span>
            </p>
            <div class="areaBox" style="border:1px solid black;padding:3px">
                
                <div class="area" v-for="(item,index) in areas" :key="index">
                    <p><span style="font-weight:bold">{{item.name}}</span>：{{item.detail}}</p>
                    <p>{{item.date}}</p>
                </div>
                <div>
                    <el-radio-group v-model="courseRadio" @change="changeCourseRadio">
                        <el-radio :label="0">确认开课</el-radio>
                        <el-radio :label="1">取消开课</el-radio>
                        <el-radio :label="2">更改具体时间{{this.courseDate}}</el-radio>
                    </el-radio-group>
                    <el-date-picker
                        v-model="courseDate"
                        type="date"
                        placeholder="选择日期"
                        v-if="this.courseRadio === 2"
                        value-format='yyyy-MM-dd'
                    >
                    </el-date-picker>
                </div>
                <!-- <p class="subtitle">学院已确认您的操作。/您的更改请求未通过，请重新选择上课时间，谢谢！</p> -->
            </div> 
        </div>
        <div class="foodContainer">
            <p style="clear:both;">
                <span class="minorTitle">食宿确定</span>
            </p>
            <div style="border:1px solid black;position:relative;padding-bottom:30px">
                <span style="font-size:18px">请选择是否需要为您安排食宿：</span>
                <el-radio-group v-model="foodRadio">
                    <el-radio :label="0">是</el-radio>
                    <el-radio :label="1">否</el-radio>
                </el-radio-group>

                <div class="areaBox" style="border:1px solid black;padding:3px">
                
                    <div class="area" v-for="(item,index) in areas" :key="index">
                        <p>城市：{{item.name}}</p>
                        <p>地点：{{item.detail}}</p>
                        <p>时间：{{item.date}}</p>
                    </div>
                </div> 
            </div>
        </div>

        <div class="fileContainer">
            <p style="clear:both;">
                <span class="minorTitle">材料办理（请上传您的签证和机票信息，以便您到达当天的接待工作，谢谢！）</span>
            </p>
            <el-upload
                class="upload-demo"
                action="https://jsonplaceholder.typicode.com/posts/"
                >
                <el-button size="small" type="primary">上传签证</el-button>
            </el-upload>
            <el-upload
                class="upload-demo"
                action="https://jsonplaceholder.typicode.com/posts/"
                >
                <el-button size="small" type="primary">上传机票</el-button>
            </el-upload>
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
                title: '等待邀请',
                description: '时间*******'
            },{
                title: '接受邀请',
                description: '时间*******'
            },{
                title: '食宿确定',
                description: '时间*******'
            },{
                title: '材料办理',
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
            }],
            fileList: [],
            commentlist: [{
                name: '罗马111',
                detail: '罗马XXXXXX酒店XXXXXXXXX房间号XXXXXXXXX',
                date: '2018年01月01日'
            },{
                name: '米兰222',
                detail: '米兰XXXXXX酒店XXXXXXXXX房间号XXXXXXXXX',
                date: '2018年01月01日'
            },{
                name: '希腊333',
                detail: '希腊XXXXXX酒店XXXXXXXXX房间号XXXXXXXXX',
                date: '2018年01月01日'
            }],
            courseRadio: 0,
            courseDate: '',
            foodRadio: 0,
        };
    },
    methods: {
        changeCourseRadio() {
            const date = new Date(1398250549490);
            const Y = date.getFullYear() + '-';
            const M = (date.getMonth()+1 < 10 ? '0'+(date.getMonth()+1) : date.getMonth()+1) + '-';
            const D = date.getDate() + ' ';
            if(this.courseRadio === 2) {
                this.courseDate = Y + M + D;
            } else {
                this.courseDate = ''
            }
            
        }
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
        flex-wrap: wrap;
    }
    .area {
        flex: 0 0 30%;
        margin-right: 10px;
        border-top: 3px solid #19568a;
    }
    .minorTitle {
        border-bottom: 3px solid #19568a;
        font-size:18px;
    }
    .upload-demo >>> .el-upload__input {
        display: none;
    }
    .containerDate {
        position: absolute;
        bottom: 3px;
        right: 10px;
    }
</style>

