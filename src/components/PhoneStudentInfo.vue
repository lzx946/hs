<template>
    <div id="login_id">
        <!--====遮罩层、加载中===-->
        <div class="modal fade bs-example-modal-lg" v-bind:class="showLoadingCss" v-on:dblclick="hideLoading()">
            <div class="spinner">
                <div class="double-bounce1"></div>
                <div class="double-bounce2"></div>
            </div>
        </div>
        <!--====================-->
        <transition name="fade">
            <div v-cloak v-if="isShowReturnInfoFlag" style="z-index: 999;" :class="{'tsama-tip-info-error':errorMessageFlag,'tsama-tip-info-success':!errorMessageFlag}">
                <div>
                    <span style="padding-left:1em;line-height: 50px;color: white;">{{returnMessage}}</span><span class="close" v-on:click="closeInfo()"></span>
                </div>
            </div>
        </transition>
        <!-- main -->
        <div style="overflow: hidden;margin-top: 70px;">
            <!-- right content -->
            <div style="background: #ECECEC;width: 100%;height: 100%;min-height: 1280px;padding: 0.1em 1em; padding-bottom: 20em;">
                <h3>个人信息</h3>
                <div style="margin-top: 50px;">
                    <div><span style="font-size: 1.3em;"><b>背景/头像</b></span></div>
                    <div style="text-align: center;margin-left: auto;margin-right: auto;"><img :src="imgUrl" style="height: 8em;width:8em;border-radius: 50%;border: 2px solid white;margin-top: 44px;" alt="暂无头像图片，请上传" />
                    </div>
                    <div style="clear: left;margin-top: 3.5em;text-align: center;">
                        <form id="form1" method="post" enctype="multipart/form-data">
                            <a class="btn btn-info" style="position: relative;cursor: pointer;">更改背景/头像
                            <input type="file" hidden="hidden" @change="updateImg()" name="uploadFile" id="uploadFile"
                                   style="opacity: 0;position: absolute;width: 8em;top: 0;height: 2.5em;left: 0;right: 0;bottom: 0;">
                        </a>
                        </form>
                    </div>
                </div>
                <div style="margin-top: 50px;">
                    <!--<div><span style="font-size: 1.3em;"><b>账户</b></span></div>
					<div style="padding: 1em;position: relative;">
						<label for="inputAccount" style="float: left;line-height: 35px;">账号</label>
						<input type="text" id="inputAccount" class="form-control" style="width: 300px;margin-left: 110px;" readonly="readonly" v-model="account" placeholder="">
						<label style="position: absolute;top: 20px;left: 430px;">账号不可修改</label>
					</div>-->
                    <div style="padding: 1em;position: relative;">
                        <label for="inputNameCN" style="float: left;line-height: 35px;">中文名<span
                            style="position: absolute;color: red;margin-top: 3px;font-size: 1.1em;margin-left: 55px;">*</span></label>
                        <input type="text" v-on:blur="toBlur(0)" v-on:focus="toFocus(0)" id="inputNameCN" class="form-control" style="width: 70%;margin-left: 110px;" v-model="cnName" placeholder="请输入您的中文名">
                        <transition name="fade">
                            <label v-cloak v-if="cnNameErrorNull" style="position: absolute;top: 20px;left: 430px;color: red">（必须）</label>
                        </transition>
                    </div>
                    <!--<div style="padding: 1em;position: relative;">
						<label for="inputNameEN" style="float: left;line-height: 35px;">英文名<span
                            style="position: absolute;color: red;margin-top: 3px;font-size: 1.1em;margin-left: 55px;">*</span></label>
						<input type="text" v-on:blur="toBlur(1)" v-on:focus="toFocus(1)" id="inputNameEN" class="form-control" style="width: 300px;margin-left: 110px;" v-model="enName" placeholder="请输入您的英文名">
						<transition name="fade">
							<label v-cloak v-if="enNameErrorNull" style="position: absolute;top: 20px;left: 430px;color: red">（必须）</label>
						</transition>
					</div>-->
                </div>
                <div style="margin-top: 50px;">
                    <div><span style="font-size: 1.3em;"><b>联系信息</b></span></div>
                    <div style="padding: 1em;position: relative;">
                        <label for="inputPhone" style="float: left;line-height: 35px;">手机号码<span
                            style="position: absolute;color: red;margin-top: 3px;font-size: 1.1em;margin-left: 41px;">*</span></label>
                        <input type="phone" id="inputPhone" class="form-control" style="width: 70%;margin-left: 110px;" readonly="readonly" v-model="phone" placeholder="请输入您的手机号">
                    </div>
                    <!--<div style="padding: 1em;position: relative;">
						<label for="inputEmail" style="float: left;line-height: 35px;">邮箱(登录)<span
                            style="position: absolute;color: red;margin-top: 3px;font-size: 1.1em;margin-left: 31px;">*</span></label>
						<input type="email" id="inputEmail" class="form-control" style="width: 300px;margin-left: 110px;" readonly="readonly" v-model="email" placeholder="请输入您的邮箱">
						<a class="tsama-fix-eamil-a" v-on:click="fixEmailClick()">修改邮箱地址</a>
						<div :class="{'tsama-sanjiaoxing':!isShowFixEmailFlag,'tsama-sanjiaoxing-top':isShowFixEmailFlag}"></div>
					</div>
					<transition name="fade">
						<div v-cloak style="padding: 1em;position: relative;margin-left: 110px;" v-if="isShowFixEmailFlag">
							<label for="inputEmailNew" style="float: left;line-height: 35px;">邮箱(新)<span
                                style="position: absolute;color: red;margin-top: 3px;font-size: 1.1em;margin-left: 45px;">*</span></label>
							<input type="email" v-on:blur="toBlur(2)" v-on:focus="toFocus(2)" id="inputEmailNew" class="form-control" style="width: 300px;margin-left: 110px;" v-model="emailNew" placeholder="请输入您的新邮箱地址">
							<transition name="fade">
								<a v-cloak v-if="!emailNewErrorNull&&!emailNewErrorFormat&&!emailNewErrorIsExist" class="tsama-fix-eamil-a" v-on:click="toFixEmail()">提交修改</a>
								<label v-cloak v-if="emailNewErrorNull" style="position: absolute;top: 20px;left: 430px;color: red">（必须）</label>
								<label v-cloak v-if="emailNewErrorFormat" style="position: absolute;top: 20px;left: 430px;color: red">（邮箱格式错误）</label>
								<label v-cloak v-if="emailNewErrorIsExist" style="position: absolute;top: 20px;left: 430px;color: red">（邮箱已存在）</label>
							</transition>

						</div>
					</transition>-->
                </div>

                <div style="margin-top: 50px;">
                    <div><span style="font-size: 1.3em;"><b>其他信息</b></span></div>
                    <div style="padding: 1em;position: relative;">
                        <label for="inputMainPoster" style="float: left;line-height: 35px;">职位<span
                                style="position: absolute;color: red;margin-top: 3px;font-size: 1.1em;margin-left: 69px;">*</span></label>
                        <input type="text" v-on:blur="toBlur(4)" v-on:focus="toFocus(4)" id="inputMainPoster" class="form-control" style="width: 70%;margin-left: 110px;" v-model="title" placeholder="请输入您的职位">
                        <transition name="fade">
                            <label v-cloak v-if="mainPosterErrorNull" style="position: absolute;top: 20px;left: 430px;color: red">（必须）</label>
                        </transition>
                    </div>
                    <div style="padding: 1em;position: relative;">
                        <div>
                            <label for="inputOtherPoster" style="float: left;line-height: 35px;">公司<span
                                style="position: absolute;color: red;margin-top: 3px;font-size: 1.1em;margin-left: 69px;">*</span></label>
                            <div v-cloak>
                                <input type="text" v-on:blur="toBlur(14)" v-on:focus="toFocus(14)" class="form-control" style="width: 70%;margin-left: 110px;margin-bottom: 10px;" v-model="department" placeholder="请输入您的工作单位">
                                <transition name="fade">
                                    <label v-cloak v-if="departmentErrorNull" style="position: absolute;top: 20px;left: 430px;color: red">（必须）</label>
                                </transition>
                                <!--<a v-if="lastIndex(index)" style="line-height: 35px;cursor: pointer;position:absolute; left:430px;top: 15px;display: inline;" v-on:click="removeOthersPoster(index)">移除</a>-->
                            </div>
                        </div>
                        <!--<div id="">
                                <a style="margin-left: 115px;line-height: 35px;cursor: pointer;" v-on:click="addOthersPoster()">添加</a>
                            </div>-->

                    </div>
                    <!--<div style="padding: 1em;position: relative;">
						<label for="inputMotto" style="float: left;line-height: 35px;">一言一语<span
                            style="position: absolute;color: red;margin-top: 3px;font-size: 1.1em;margin-left: 41px;">*</span></label>
						<input type="text" v-on:blur="toBlur(5)" v-on:focus="toFocus(5)" id="inputMotto" class="form-control" style="width: 300px;margin-left: 110px;" v-model="motto" placeholder="人生中最重要的一句话">
						<transition name="fade">
							<label v-cloak v-if="mottoErrorNull" style="position: absolute;top: 20px;left: 430px;color: red">（必须）</label>
						</transition>
					</div>-->
                    <div style="padding: 1em;position: relative;">
                        <label for="inputIntroduction" style="float: left;line-height: 35px;">个人简介<span
                            style="position: absolute;color: red;margin-top: 3px;font-size: 1.1em;margin-left: 41px;">*</span></label>
                        <textarea type="text" v-on:blur="toBlur(6)" v-on:focus="toFocus(6)" id="inputIntroduction" class="form-control" style="width: 70%;margin-left: 110px;height: 100px;" v-model="introduction" placeholder="个人简介"></textarea>
                        <transition name="fade">
                            <label v-cloak v-if="introductionErrorNull" style="position: absolute;top: 20px;left: 430px;color: red">（必须）</label>
                        </transition>
                    </div>
                </div>
                <div style="margin-top: 50px;">
                    <div><span style="font-size: 1.3em;"><b>账户管理</b></span></div>
                    <div style="padding: 1em;position: relative; overflow: hidden;">
                        <label for="inputNewPassword" style="float: left;line-height: 35px;">密码管理</label>
                        <a style="line-height: 35px;cursor: pointer;position:absolute; left:130px;top: 15px;display: inline;" v-if="!isShowFixPasswordFlag" v-on:click="isShowFixPasswordFlag=!isShowFixPasswordFlag">修改密码</a>
                        <a style="line-height: 35px;cursor: pointer;position:absolute; left:130px;top: 15px;display: inline;" v-if="isShowFixPasswordFlag" v-on:click="isShowFixPasswordFlag=!isShowFixPasswordFlag">取消</a>
                    </div>
                    <transition name="fade">
                        <div v-cloak style="padding: 1em;position: relative;" v-if="isShowFixPasswordFlag">
                            <label for="inputPassword" style="float: left;line-height: 35px;">新密码<span
                                style="position: absolute;color: red;margin-top: 3px;font-size: 1.1em;margin-left: 55px;">*</span></label>
                            <input type="password" v-on:blur="toBlur(7)" v-on:focus="toFocus(7)" id="inputPassword" class="form-control" style="width: 40%;margin-left: 110px;" v-model="newPassword" placeholder="请输入您的新密码">
                            <label for="inputPassword" style="float: left;line-height: 35px;margin-left: -42px;">再次输入<span
                                style="position: absolute;color: red;margin-top: 3px;font-size: 1.1em;margin-left: 41px;">*</span></label>
                            <input type="password" v-on:blur="toBlur(8)" v-on:focus="toFocus(8)" id="inputRePassword" class="form-control" style="width: 40%;margin-left: 110px;" v-model="reNewPassword" placeholder="请再次输入您的新密码">
                            <transition name="fade">
                                <a v-cloak v-if="!passwordErrorNull&&!passwordErrorLength&&!rePasswordErrorNoEq" class="tsama-fix-password-a" v-on:click="fixPassword()">提交新密码</a>
                                <label v-cloak v-if="passwordErrorNull" style="position: absolute;top: 20px;left: 75%;color: red">（必须）</label>
                                <label v-cloak v-if="passwordErrorLength" style="position: absolute;top: 20px;left: 75%;color: red">（密码长度为6-20位）</label>
                                <label v-cloak v-if="rePasswordErrorNoEq" style="position: absolute;top: 55px;left: 75%;color: red">（两次密码输入不一致）</label>
                            </transition>

                        </div>
                    </transition>
                </div>
                <button class="btn btn-primary" @click="update()">提交更改</button>
                 <a @click="logout()" style="text-align: center;border: none;cursor:pointer;margin-left: 100px;">注销登录</a>
            </div>
        </div>
    </div>
</template>

<script>
    import logoImgSrc from '@/assets/logo.png'
    import { config } from '@/util/config.js'
    import { common } from '@/util/common.js'
    export default {
        name: 'StudentInfo',
        data() {
            return {
                active: 0,
                imgUrl: "",
                account: "liter7",

                isShowReturnInfoFlag: false,
                errorMessageFlag: false,
                returnMessage: "",

                cnName: "",
                cnNameErrorNull: false,

                enName: "",
                enNameErrorNull: false,

                phone: "",

                //				email: "123@gamil.com",
                //
                //				emailNew: "",
                //				emailNewErrorFormat: false,
                //				emailNewErrorNull: false,
                //				emailNewErrorIsExist: false,
                //
                //				emailG: "",
                //				emailGErrorFormat: false,
                //				emailGErrorNull: false,

                title: "",
                mainPosterErrorNull: false,

                department: '',
                othersPosterNowIndex: 100,
                departmentErrorNull: false,

                motto: "",
                mottoErrorNull: false,

                introduction: "",
                introductionErrorNull: false,

                newPassword: "",
                reNewPassword: "",
                passwordErrorLength: false,
                passwordErrorNull: false,
                rePasswordErrorNoEq: false,

                isShowFixPasswordFlag: false,
                //				isShowFixEmailFlag: false,

                showLoadingCss: {
                    "in": false,
                    "showloading": false
                },
                logoImgSrc: logoImgSrc,
            }
        },
        created() {
            common.isLogin();
            if(common.token == null) {
                this.$router.push('/phone/login')
            } else {
                var _self = this;
                this.showLoading();
                $.ajax({
                    url: config.IP + "/student/getStudentlist",
                    data: {
                        id: common.token.id
                    },
                    type: "post",
                    success: function(data) {
                        if((typeof data) != 'object') {
                            data = JSON.parse(data)
                        }
                        data = data.objectList[0];
//                      _self.account = data.account;
                        if(data.realname) {
                            _self.cnName = data.realname;
                        }
                        if(data.enname) {
                            _self.enName = data.enname;
                        }
                        if(data.motto) {
                            _self.motto = data.motto;
                        }
                        if(data.position) {
                            _self.title = data.position;
                        }

                        if(data.summary) {
                            _self.introduction = data.summary;
                        }
                        if(data.url) {
                            _self.imgUrl = data.url;
                        }
                        if(data.phone) {
                            _self.phone = data.phone;
                        }
                        if(data.company) {
                            _self.department = data.company;
                        }
                        _self.hideLoading();
                    },
                    error: function(data, message) {
                        _self.errorMessageFlag = true;
                        _self.returnMessage = "查询失败，请稍后再试";
                        _self.isShowReturnInfoFlag = true;
                        _self.hideLoading();
                        setTimeout(function() {
                            _self.isShowReturnInfoFlag = false;
                        }, 3000);
                    }
                })
            }
        },
        methods: {
            logout: function() {
                common.logout();
                this.isLoginFlag = false;
                this.$router.push('/phone/login')
            },
            updateImg: function() {
                var _self = this;
                this.showLoading();
                var formData = new FormData(document.getElementById("form1"));
                $.ajax({
                    //几个参数需要注意一下
                    type: "POST", //方法类型
                    url: config.IP + "/file/upload.do", //url
                    data: formData,
                    cache: false,
                    contentType: false,
                    processData: false,
                    success: function(result) {
                        result = JSON.parse(result)
                        if(result.flag == 1) {
                            //                            这里不能直接删
                            //                            $.ajax({
                            //                                //几个参数需要注意一下
                            //                                type: "POST",//方法类型
                            //                                url: config.IP+"/file/delete.do" ,//url
                            //                                data: {
                            //                                    id:token.photoid
                            //                                },
                            //                                cache: false,
                            //                                contentType: false,
                            //                                processData: false,
                            //                                success: function (result) {
                            //                                    console.log(result);
                            //                                    result = JSON.parse(result)
                            //                                    if(result.flag==1){
                            //                                        _self.imgUrl=result.objectList.url;
                            //                                        alert("添加成功，请点击最下方提交更改按钮！");
                            //                                    }
                            //                                    _self.hideLoading();
                            //                                },
                            //                                error : function() {
                            //                                    alert("上传失败，请稍后重试！");
                            //                                    _self.hideLoading();
                            //                                }
                            //                            });
                            common.token.photoid = result.objectList.id;
                            _self.imgUrl = result.objectList.url;
                            alert("添加成功，请点击最下方提交更改按钮！");
                        }
                        _self.hideLoading();
                    },
                    error: function() {
                        alert("上传失败，请稍后重试！");
                        _self.hideLoading();
                    }
                });
            },
            update: function() {
                this.toBlur(0);
                this.toBlur(4);
                this.toBlur(6);
                this.toBlur(14);
                if(this.cnNameErrorNull 
                     || this.introductionErrorNull || this.mainPosterErrorNull || this.departmentErrorNull) {
                    return;
                }
                var _self = this;
                this.showLoading();
                $.ajax({
                    url: config.IP + "/student/updateStudentinfo",
                    data: {
                        id: common.token.id,
                        realname: this.cnName,
                        position: this.title,
                        summary: this.introduction,
                        company: this.department,
                        photoid: common.token.photoid
                    },
                    type: "post",
                    success: function(data) {
                        data = JSON.parse(data);
                        if(data.flag == 1) {
                            _self.errorMessageFlag = false;
                            _self.returnMessage = "修改成功！";
                            _self.isShowReturnInfoFlag = true;
                            _self.hideLoading();
                            setTimeout(function() {
                                _self.isShowReturnInfoFlag = false;
                            }, 3000);
                        } else {
                            _self.errorMessageFlag = true;
                            _self.returnMessage = "查询失败，请稍后再试";
                            _self.isShowReturnInfoFlag = true;
                            _self.hideLoading();
                            setTimeout(function() {
                                _self.isShowReturnInfoFlag = false;
                            }, 3000);
                        }

                        _self.hideLoading();
                    },
                    error: function(data, message) {
                        _self.errorMessageFlag = true;
                        _self.returnMessage = "查询失败，请稍后再试";
                        _self.isShowReturnInfoFlag = true;
                        _self.hideLoading();
                        setTimeout(function() {
                            _self.isShowReturnInfoFlag = false;
                        }, 3000);
                    }
                })
            },
            fixPassword: function() {
                this.toBlur(7);
                this.toBlur(8);
                if(this.passwordErrorLength || this.passwordErrorNull || this.rePasswordErrorNoEq) {
                    return;
                }
                var _self = this;
                this.showLoading();

                $.ajax({
                    url: config.IP + "/student/updateStudentinfo",
                    data: {
                        id: common.token.id,
                        password: md5(this.newPassword)
                    },
                    type: "post",
                    success: function(data) {
                        data = JSON.parse(data);
                        if(data.flag == 1) {
                            _self.errorMessageFlag = false;
                            _self.returnMessage = "修改密码成功！";
                            _self.isShowReturnInfoFlag = true;
                            _self.hideLoading();
                            setTimeout(function() {
                                _self.isShowReturnInfoFlag = false;
                            }, 3000);
                        } else {
                            _self.errorMessageFlag = true;
                            _self.returnMessage = "修改失败，请稍后再试";
                            _self.isShowReturnInfoFlag = true;
                            _self.hideLoading();
                            setTimeout(function() {
                                _self.isShowReturnInfoFlag = false;
                            }, 3000);
                        }

                        _self.hideLoading();
                    },
                    error: function(data, message) {
                        _self.errorMessageFlag = true;
                        _self.returnMessage = "修改失败，请稍后再试";
                        _self.isShowReturnInfoFlag = true;
                        _self.hideLoading();
                        setTimeout(function() {
                            _self.isShowReturnInfoFlag = false;
                        }, 3000);
                    }
                })
            },
            lastIndex: function(index) {
                return(index == this.othersPosterList.length - 1)
            },
            addOthersPoster: function() {
                var item = {
                    "value": ""
                }
                this.othersPosterList.unshift(item);
            },
            removeOthersPoster: function() {
                this.othersPosterList.splice(0, 1);
            },
            closeInfo: function() {
                this.isShowReturnInfoFlag = false;
            },
            getInfo: function(index) {
                //获取个人信息
                if(index == 0) {
                    this.active = 0;
                }
            },
            //			fixEmailClick: function() {
            //				this.isShowFixEmailFlag = !this.isShowFixEmailFlag;
            //			},
            toBlur: function(index) {
                var _self = this;
                if(index == 0) {
                    if(this.cnName.trim() == "") {
                        this.cnNameErrorNull = true;
                        return;
                    }
                }
                if(index == 1) {
                    if(this.enName.trim() == "") {
                        this.enNameErrorNull = true;
                        return;
                    }
                }
                //				if(index == 2) {
                //					if(this.emailNew.trim() == "") {
                //						this.emailNewErrorNull = true;
                //						return;
                //					}
                //					/*格式是否正确*/
                //					if(!tsamaEmailReg.test(this.emailNew)) {
                //						this.emailNewErrorFormat = true;
                //						return;
                //					}
                //					/*验证邮箱是否存在*/
                //					$.ajax({
                //						url: config.IP + "/yanzhengS",
                //						data: {
                //							email: this.emailNew
                //						},
                //						async: false,
                //						type: "post",
                //						success: function(data) {
                //							if(data == true) {
                //								_self.emailNewErrorIsExist = true;
                //							}
                //						},
                //						error: function(data, message) {}
                //					})
                //				}

                if(index == 4) {
                    if(this.title.trim() == "") {
                        this.mainPosterErrorNull = true;
                        return;
                    }
                }
                if(index == 5) {
                    if(this.motto.trim() == "") {
                        this.mottoErrorNull = true;
                        return;
                    }
                }
                if(index == 6) {
                    if(this.introduction.trim() == "") {
                        this.introductionErrorNull = true;
                        return;
                    }
                }
                if(index == 7) {
                    if(this.newPassword.trim() == "") {
                        this.passwordErrorNull = true;
                        return;
                    }
                    if(this.newPassword.length < 6 || this.newPassword.length > 20) {
                        this.passwordErrorLength = true;
                        return;
                    }
                }
                if(index == 8) {
                    if(this.reNewPassword != this.newPassword) {
                        this.rePasswordErrorNoEq = true;
                        return;
                    }
                }
                if(index == 14) {
                    if(this.department.trim() == "") {
                        this.departmentErrorNull = true;
                        return;
                    }
                }
            },
            toFocus: function(index) {
                if(index == 0) {
                    this.cnNameErrorNull = false;
                    return;
                }
                if(index == 1) {
                    this.enNameErrorNull = false;
                    return;
                }
                //				if(index == 2) {
                //					this.emailNewErrorNull = false;
                //					this.emailNewErrorFormat = false;
                //					this.emailNewErrorIsExist = false;
                //					return;
                //				}

                if(index == 4) {
                    this.mainPosterErrorNull = false;
                    return;
                }
                if(index == 5) {
                    this.mottoErrorNull = false;
                    return;
                }
                if(index == 6) {
                    this.introductionErrorNull = false;
                    return;
                }
                if(index == 7) {
                    this.passwordErrorNull = false;
                    this.passwordErrorLength = false;
                    return;
                }
                if(index == 8) {
                    this.rePasswordErrorNoEq = false;
                    return;
                }
                if(index == 14) {
                    this.departmentErrorNull = false;
                    return;
                }
            },
            //			toFixEmail: function() {
            //				this.toBlur(2);
            //				if(this.emailNewErrorNull || this.emailNewErrorFormat || this.emailNewErrorIsExist) {
            //					return;
            //				}
            //				var _self = this;
            //				this.showLoading();
            //				$.ajax({
            //					url: config.IP + "/student/updateStudentinfo",
            //					data: {
            //						id: token.id,
            //						email: this.emailNew
            //					},
            //					type: "post",
            //					success: function(data) {
            //						data = JSON.parse(data);
            //						if(data.flag == 1) {
            //							_self.errorMessageFlag = false;
            //							_self.returnMessage = "修改邮箱成功！";
            //							_self.isShowReturnInfoFlag = true;
            //							_self.hideLoading();
            //							setTimeout(function() {
            //								_self.isShowReturnInfoFlag = false;
            //							}, 3000);
            //						} else {
            //							_self.errorMessageFlag = true;
            //							_self.returnMessage = "修改失败，请稍后再试";
            //							_self.isShowReturnInfoFlag = true;
            //							_self.hideLoading();
            //							setTimeout(function() {
            //								_self.isShowReturnInfoFlag = false;
            //							}, 3000);
            //						}
            //
            //						_self.hideLoading();
            //					},
            //					error: function(data, message) {
            //						_self.errorMessageFlag = true;
            //						_self.returnMessage = "修改失败，请稍后再试";
            //						_self.isShowReturnInfoFlag = true;
            //						_self.hideLoading();
            //						setTimeout(function() {
            //							_self.isShowReturnInfoFlag = false;
            //						}, 3000);
            //					}
            //				})
            //			},

            /**
             * 隐藏加载中页面
             */
            hideLoading: function() {
                this.showLoadingCss.in = false;
                this.showLoadingCss.showloading = false;
            },
            /**
             * 显示加载中页面
             */
            showLoading: function() {
                this.showLoadingCss.in = true;
                this.showLoadingCss.showloading = true;
            }
        }
    }
</script>

<style>
    [v-cloak] {
        display: none;
    }
    
    body {}
    
    .tsama-info-left-menu {
        height: 3em;
        width: 100%;
        line-height: 3em;
        color: white;
    }
    
    .tsama-info-left-menu:hover {
        background: #19568a;
        cursor: pointer;
    }
    
    .tsama-info-left-menu-active {
        background: #19568a;
        cursor: pointer;
    }
    
    .tsama-sanjiaoxing {
        display: inline;
        border-top: 8px solid #5BC0DE;
        border-bottom: 8px solid transparent;
        border-left: 8px solid transparent;
        border-right: 8px solid transparent;
        position: absolute;
        left: 520px;
        top: 27px;
        transition: border 0.5s;
    }
    
    .tsama-sanjiaoxing-top {
        display: inline;
        border-top: 8px solid transparent;
        border-bottom: 8px solid #5BC0DE;
        border-left: 8px solid transparent;
        border-right: 8px solid transparent;
        position: absolute;
        left: 520px;
        top: 18px;
        transition: border 0.5s;
    }
    
    .tsama-fix-eamil-a {
        cursor: pointer;
        position: absolute;
        top: 20px;
        left: 430px;
    }
    
    .tsama-fix-password-a {
        cursor: pointer;
        position: absolute;
        top: 55px;
        left: 75%;
    }
    
    .fade-enter-active,
    .fade-leave-active {
        transition: opacity .8s;
    }
    
    .fade-enter,
    .fade-leave-to {
        opacity: 0;
    }
    
    .tsama-tip-info-success {
        position: fixed;
        top: 100px;
        right: 0;
        width: 200px;
        height: 50px;
        background: #419641;
        border-radius: 5px;
    }
    
    .tsama-tip-info-error {
        position: fixed;
        top: 100px;
        right: 0;
        width: 200px;
        height: 50px;
        background: #eb9316;
        border-radius: 5px;
    }
    /*========================关闭图标====================*/
    
    .close {
        color: #000000;
        line-height: 20px;
        text-align: center;
        height: 20px;
        width: 20px;
        font-size: 18px;
        padding: 1px;
    }
    
    .close::before {
        content: "\2716";
    }
    
    .close {
        top: 15px;
        right: 10px;
        position: absolute;
    }
    /*==================================================*/
</style>