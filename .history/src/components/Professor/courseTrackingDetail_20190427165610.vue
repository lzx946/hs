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
            <p style="clear:both;">
                <span class="minorTitle">课程内容</span>
            </p>
            <p style="text-indent:2em;">
没有人知道失败和成功间的差距是多么得小。它们之间只相差了一个词的距离，那就是胆怯。问一问福特，问一问爱迪生，问一问所有已经获得成功的人，他们会告诉你，把失败从成功中分割开的裂沟是多么得狭窄，也会明确地告诉你，依靠坚持和信念必然可以让人从失败走向成功。
即使是最平凡的人，也是得要去为他那个世界的存在而战斗。越长大，越是小心翼翼，想要活得爽，大家都劝你不要在乎别人的评价。但不是每个人都能做到这一点，既然做不到不在乎外界的评价，那就请把自己手头的事都尽心尽力给做好。
生活坏到一定程度就会好起来，因为它无法更坏。许多事情，坚持坚持，就过来了。不要羡慕别人，不是每个人都那么完美，只是你没看到罢了。再苦再累，只要坚持往前走，属于你的风景终会出现。人生就是一场漫长的对抗，有些人笑在开始，有些人却赢在最终。命运不会偏爱谁，就看你能够追逐多久，坚持多久。</p>
        </div>

        <div class="resultContainer">
            <p style="clear:both;">
                <span class="minorTitle">审核结果</span>
            </p>
            <div style="border:1px solid black">
                <p style="font-size:18px">XXX教授：</p>
                <p style="text-indent:2em;">您好！您申请的XXX课程已经通过审核，请尽快上传课程材料、办理签证、机票等相关手续，完成后续工作。您申请的XXX课程已经通过审核，请尽快上传课程材料、办理签证、机票等相关手续，完成后续工作。您申请的XXX课程已经通过审核，请尽快上传课程材料、办理签证、机票等相关手续，完成后续工作。您申请的XXX课程已经通过审核，请尽快上传课程材料、办理签证、机票等相关手续，完成后续工作。</p>
                
                <p class="containerDate"><span style="margin-right: 20px">审核人：XXXX</span><span>2019-03-26 10:43:57</span></p>
            </div>
        </div>

        <div class="fileContainer">
            <p style="clear:both;">
                <span class="minorTitle">材料上传 （请上传课程所需PPT或文档）</span>
            </p>
            <div style="border:1px solid black;padding:10px">
                <el-upload
                    class="upload-demo"
                    action="https://jsonplaceholder.typicode.com/posts/"
                    :on-preview="handlePreview"
                    :on-remove="handleRemove"
                    :before-upload="beforeUpload"
                    multiple
                    :limit="3"
                    :on-exceed="handleExceed"
                    :file-list="fileList">
                    <el-button size="small" type="primary">点击上传</el-button>
                    <div slot="tip" class="el-upload__tip">只能上传jpg/png文件，且不超过500kb</div>
                </el-upload>
            </div>
        </div>

        <div class="commentContainer">
            <p style="clear:both;">
                <span class="minorTitle">评论列表</span>
            </p>
            <div style="border:1px solid black" v-for="(item, index) in commentlist" :key="index">
                <p style="font-size:18px">{{item.name}}：</p>

                <p style="text-indent:2em;">{{item.detail}}</p>
                <p class="containerDate">{{item.date}}</p>
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
            }]
        };
    },
    methods: {
        handleRemove(file, fileList) {
            console.log(file, fileList);
        },
        handlePreview(file) {
            console.log(file);
        },
        handleExceed(files, fileList) {
            this.$message.warning(`当前限制选择 3 个文件，本次选择了 ${files.length} 个文件，共选择了 ${files.length + fileList.length} 个文件`);
        },
        beforeUpload(file) {
            console.log(file)
            const isPPT_Word = file.type.includes('ppt') || file.type.includes('word');
            const isLt = file.size / 1024  < 500;

            if (!isPPT_Word) {
            this.$message.error('上传课程所需PPT或文档');
            }
            if (!isLt) {
            this.$message.error('上传文件大小不能超过 500KB!');
            }
            return isPPT_Word && isLt;
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
        float: right;
        padding-bottom: 30px;
    }
    .containerDate::after {
        clear:both;
    }
</style>

