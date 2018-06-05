<template>
    <div class="login_form">
        <div class="login_left">
            <p style="padding-top:150px;">{{$t('uc.regist.hasaccount')}}</p>
            <router-link to="login">
                <Button style="background:#1E2125;width:130px;margin-top:50px;color:#fff;">{{$t('uc.regist.login')}}</Button>
            </router-link>
            <div class="login_right" style="padding:20px 30px;">
                <Form v-if="allowRegister" ref="formInline" :model="formInline" :rules="ruleInline" inline>
                    <FormItem style="text-align:center;">
                        <ButtonGroup>
                            <Button v-for="(list,index) in buttonLists" :key="list.text" :class="{ active:changeActive == index}" @click="actives(index)">{{list.text}}</Button>
                        </ButtonGroup>
                    </FormItem>
                    <FormItem prop="username">
                        <Input type="text" v-model="formInline.username" :placeholder="$t('uc.regist.username')">

                        </Input>
                    </FormItem>
                    <FormItem prop="country">
                        <Select v-model="formInline.country" :placeholder="$t('uc.regist.country')" @on-change="onAreaChange">
                            <Option v-for="area in areas" :value="area.zhName">{{area.zhName}}</Option>
                        </Select>
                    </FormItem>
                    <FormItem prop="user">
                        <Input v-if="changeActive == 0" type="text" v-model="formInline.user" :placeholder="key">
                            <span slot="prepend">+{{formInline.areaCode}}</span>
                        </Input>
                        <Input v-else type="text" v-model="formInline.user" :placeholder="key">
                        </Input>
                    </FormItem>

                    <FormItem prop="code" v-show="showCode">
                        <Input style="width:68%" type="text" v-model="formInline.code" :placeholder="$t('uc.regist.smscode')">

                        </Input>
                        <input id="sendCode" @click="sendCode();" type="Button" :value="$t('uc.regist.sendcode')">

                        </input>
                    </FormItem>
                    <FormItem prop="password">
                        <Input type="password" v-model="formInline.password" :placeholder="$t('uc.regist.pwd')">

                        </Input>
                    </FormItem>
                    <FormItem prop="agentcode">
                        <Input type="text" v-model="formInline.agentcode" :placeholder="$t('uc.regist.agentcode')">

                        </Input>
                    </FormItem>
                    <div style="color:#979797;display:inline-block;line-height:30px;font-size:12px;cursor:default">
                        <label>
                            <Checkbox v-model="agree">{{$t('uc.regist.agreement')}}</Checkbox>
                        </label>
                        <a href="#/about-protocol" target="_blank" style="color:#000;">《{{$t('uc.regist.userprotocol')}}》</a>
                    </div>
                    <FormItem>
                        <Button style="width:100%;" type="info" @click="handleSubmit('formInline')" :disabled="registing">{{$t('uc.regist.regist')}}</Button>
                    </FormItem>
                </Form>
                <Alert v-else type="warning">
                    Coming soon!
                    <template slot="desc">
                        CEX will open register in Mar 1st
                    </template>
                </Alert>
            </div>
        </div>
      <Modal v-model="modal1" :mask-closable="false">
        <p slot="header" style="text-align:center">{{$t('uc.regist.modaltitle')}}</p>
        <div style="text-align:center">
          <div>
            <div id="captcha">
                <p id="wait" class="show">{{$t('uc.login.validatecodeload')}}......</p>
            </div>
          </div>
          <p id="notice" class="hide">{{$t('uc.login.validatemsg')}}</p>
        </div>
        <p slot="footer"></p>
      </Modal>
    </div>
</template>
<style scoped>
  /* 验证码 */
  #captcha {
    width: 100%;
    display: inline-block;
  }
  .show {
    display: block;
  }
  .hide {
    display: none;
  }
  #notice {
    color: red;
  }
  #wait {
    text-align: left;
    color: #666;
    margin: 0;
  }
</style>
<script>
  import gtInit from '../../assets/js/gt.js';
  import $ from 'jquery';
    export default {
        data () {
            const validateUser = (rule, value, callback) => {
                if(this.changeActive==0){
                    var reg = /^[1][3,4,5,6,7,8,9][0-9]{9}$/;
                    if(value==''){
                        callback(new Error(this.$t('uc.regist.teltip')))
                    }else if(!reg.test(this.formInline.user)){
                        callback(new Error(this.$t('uc.regist.telerr')));
                    }else{
                        callback();
                    }
                }else{
                    var reg = /^[a-z0-9]+([._\\-]*[a-z0-9])*@([a-z0-9]+[-a-z0-9]*[a-z0-9]+.){1,63}[a-z0-9]+$/;
                    reg = /^(\w)+(\.\w+)*@(\w)+((\.\w{2,3}){1,3})$/;
                    if(value==''){
                        callback(new Error(this.$t('uc.regist.emailtip')))
                    }else if(!reg.test(this.formInline.user)){
                        callback(new Error(this.$t('uc.regist.emailerr')));
                    }else{
                        callback();
                    }
                }
            };
            const validateRepassword = (rule, value, callback) => {
                    if (value === '') {
                        callback(new Error(this.$t('uc.regist.confirmpwdtip')));
                    } else if (value !== this.formInline.password) {
                        callback(new Error(this.$t('uc.regist.confirmpwderr')));
                    } else {
                        callback();
                    }
            };
            return {
                registing:false,
                captchaObj:null,
                modal1:false,
                _captchaResult:null,
                agree:true,
                allowRegister:true,
                buttonLists:[
                    {
                        "text":this.$t('uc.regist.telregist')
                    },
                    {
                        "text":this.$t('uc.regist.emailregist')
                    }
                ],
                areas:[],
                changeActive:0,
                showCode:true,
                countdown:60,
                formInline: {
                    username:'',
                    country:'',
                    user: '',
                    code:'',
                    areaCode:'',
                    password: '',
                    repassword:'',
                    agentcode:((typeof this.$route.query.agent == "undefined") ? '' : this.$route.query.agent),
                },
                ruleInline: {
                    username: [
                        { required: true, message: this.$t('uc.regist.usernametip'), trigger: 'blur' },
                        { type: 'string', min: 3, max: 15, message: this.$t('uc.regist.usernamemsg'), trigger: 'blur' }
                    ],
                    country: [
                        { required: true, message: this.$t('uc.regist.countrytip'), trigger: 'blur' }
                    ],
                    user: [
                        { validator: validateUser, trigger: 'blur' }
                    ],
                    code: [
                        { required: true, message: this.$t('uc.regist.smscodetip'), trigger: 'blur' }
                    ],
                    password: [
                        { required: true, message: this.$t('uc.regist.pwdtip'), trigger: 'blur' },
                        { type: 'string', min: 6, message: this.$t('uc.regist.pwdmsg'), trigger: 'blur' }
                    ],
                    repassword: [
                        { validator: validateRepassword, trigger: 'blur' }
                    ]
                },
                key:'',
                code:''
            }
        },
        watch:{
            changeActive:function(val){
                this.$refs['formInline'].resetFields();
                // if (val == 0) this.initGtCaptcha();
　　　　　　  },
          'lang':function () {
            this.updateLangData();
          }
        },
        computed: {
          'lang': function () {
            return this.$store.state.lang;
          },
          'isLogin': function() {
            return this.$store.getters.isLogin;
          },
        },
        created:function(){
            this.init();
            this.actives(this.changeActive);
        },
        methods: {
          updateLangData(){
            this.buttonLists = [
              {
                "text":this.$t('uc.regist.telregist')
              },
              {
                "text":this.$t('uc.regist.emailregist')
              }
            ]

            if(this.changeActive==0){
              this.key=this.$t('uc.regist.telno');
            }else{
              this.key=this.$t('uc.regist.email');
            }
          },
            init(){
              if (this.isLogin) {
                this.$router.push('/');
              }
                this.getAreas();
                // this.initGtCaptcha();
            },
          initGtCaptcha(){
            var that = this;
            this.$http.get(this.host + this.api.uc.captcha)
              .then(function(res){
                window.initGeetest({
                  // 以下配置参数来自服务端 SDK
                  gt: res.body.gt,
                  challenge: res.body.challenge,
                  offline: !res.body.success,//表示用户后台检测极验服务器是否宕机
                  new_captcha: res.body.new_captcha,//用于宕机时表示是新验证码的宕机

                  product:"popup",
                  width:"100%"
                }, function (captchaObj){
                  captchaObj.onSuccess(function (){
                    that._captchaResult = captchaObj.getValidate();
                    that.afterValidate();
                  })
                  // 将验证码加到id为captcha的元素里，同时会有三个input的值用于表单提交
                  captchaObj.appendTo("#captcha");
                  that.captchaObj = captchaObj;
                  captchaObj.onReady(function () {
                    $("#wait").hide();
                  });
                });
              })
          },
            onAreaChange(value){
                for(var i=0;i<this.areas.length;i++){
                    if(this.areas[i].zhName == value){
                        this.formInline.areaCode = this.areas[i].areaCode;
                    }
                }
            },
            getAreas(){
                this.$http.post(this.host + this.api.common.area).then(response => {
                    var resp = response.body;
                    this.areas = resp.data;
                    this.formInline.country = this.areas[0].zhName;
                    this.formInline.areaCode = this.areas[0].areaCode;
                });
            },
            actives:function(index){
                this.changeActive=index;
                if(this.changeActive==0){
                    this.showCode=true;
                    this.key=this.$t('uc.regist.telno');
                    this.ruleInline.code=[{ required: true, message: this.$t('uc.regist.smscodetip'), trigger: 'blur' }];

                }else{
                    this.showCode=false;
                    this.key=this.$t('uc.regist.email');
                    this.ruleInline.code=[];
                }
            },
            handleSubmit(name) {
                this.$refs[name].validate((valid) => {
                    if (valid) {
                        if(this.agree==true){
                            if(this.changeActive==1){
                              this.openValidateModal();
                            }else{
                                this.registing = true;
                                var params={};
                                params['phone']=this.formInline.user;
                                params['username']=this.formInline.username;
                                params['password']=this.formInline.password;
                                params['code']=this.formInline.code;
                                params['country']=this.formInline.country;
                                params["promotion"] = this.formInline.agentcode;

                                this.$http.post(this.host+'/uc/register/phone',params).then(response => {
                                    this.registing = false;
                                    var resp=response.body;
                                    if(resp.code==0){
                                        this.$Notice.success({
                                            title: this.$t('common.tip'),
                                            desc: resp.message
                                        });
                                      var that=this;
                                        setTimeout(() => {
                                            that.$router.push('login');
                                        },3000)
                                    }else{
                                        this.$Notice.error({
                                            title: this.$t('common.tip'),
                                            desc: resp.message
                                        });
                                    }
                                })
                            }
                        }else{
                            this.$Notice.error({
                                title: this.$t('common.tip'),
                                desc: this.$t('uc.regist.agreementtip')
                            });
                        }

                    } else {

                    }
                })
            },
            settime(){
                var obj=document.getElementById('sendCode');
                if(this.countdown == 0) {
                    obj.removeAttribute("disabled");
                    obj.value = this.$t('uc.regist.sendcode');
                    this.countdown = 60;
                    return;
                }else{
                    obj.setAttribute("disabled", true);
                    obj.value = this.countdown;
                    this.countdown--;
                }
                var that=this;
                setTimeout(function() {
                    that.settime()
                }, 1000)
            },
            sendCode(){
                this.settime();
                var mobilePhone=this.formInline.user;
                if(mobilePhone==""){
                    this.countdown=0;
                    this.$Notice.error({
                        title: this.$t('common.tip'),
                        desc: this.$t('uc.regist.teltip')
                    });
                    return;
                }
                var country = this.formInline.country;
                if(mobilePhone==""){
                  this.countdown=0;
                  this.$Notice.error({
                    title: this.$t('common.tip'),
                    desc: '请填写国家'
                  });
                  return;
                }
                this.openValidateModal();
            },
          openValidateModal(){
            if (this.captchaObj != null && this.captchaObj.reset) {
              this.captchaObj.reset();
            }else {
              this.initGtCaptcha();
            }
            this.modal1 = true;
          },
          afterValidate(){
            this.modal1 = false;
            if(this.changeActive==1) {
              var params={};
              params['email']=this.formInline.user;
              params['password']=this.formInline.password;
              params['username']=this.formInline.username;
              params['country']=this.formInline.country;
              params['promotion']=this.formInline.agentcode;
              params["geetest_challenge"] = this._captchaResult.geetest_challenge;//极验验证二次验证表单数据 chllenge
              params["geetest_validate"] = this._captchaResult.geetest_validate;//极验验证二次验证表单数据 validate
              params["geetest_seccode"] = this._captchaResult.geetest_seccode;//极验验证二次验证表单数据 seccode

              this.$http.post(this.host+'/uc/register/email',params).then(response => {
                var resp=response.body;
                if(resp.code==0){
                  this.$Notice.success({
                    title: this.$t('common.tip'),
                    desc: resp.message
                  });
                  var that=this;
                  setTimeout(() => {
                    that.$router.push('login');
                  },3000)
                }else{
                  this.$Notice.error({
                    title: this.$t('common.tip'),
                    desc: resp.message
                  });
                }
              });
            }else {
              var params = {};
              params["phone"] = this.formInline.user;
              params["country"] = this.formInline.country;//国家中文名
              params["geetest_challenge"] = this._captchaResult.geetest_challenge;//极验验证二次验证表单数据 chllenge
              params["geetest_validate"] = this._captchaResult.geetest_validate;//极验验证二次验证表单数据 validate
              params["geetest_seccode"] = this._captchaResult.geetest_seccode;//极验验证二次验证表单数据 seccode
              this.$http.post(this.host+'/uc/mobile/code',params).then(response => {
                this.countdown=60;
                var resp=response.body;
                if(resp.code==0){
                  this.$Notice.success({
                    title: this.$t('common.tip'),
                    desc: resp.message
                  });
                }else{
                  // this.countdown=0;
                  this.$Notice.error({
                    title: this.$t('common.tip'),
                    desc: resp.message
                  });
                }
              });
            }
          }
        }
    }
</script>
