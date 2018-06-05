<template>
    <div class="login_form">
        <div class="login_left">
            <p style="padding-top:150px;">{{$t('uc.forget.hasaccount')}}</p>
            <router-link to="login">
                <Button style="background:#1E2125;width:130px;margin-top:50px;color:#fff;">{{$t('uc.forget.login')}}</Button>
            </router-link>
            <div class="login_right" style="padding:70px 30px;">
                <Form ref="formInline" :model="formInline" :rules="ruleInline" inline>
                    <FormItem style="text-align:center;">
                        <ButtonGroup>
                            <Button v-for="(list,index) in buttonLists" :key="list.text" :class="{ active:changeActive == index}" @click="actives(index)">{{list.text}}</Button>
                        </ButtonGroup>
                    </FormItem>
                    <FormItem prop="user">
                        <Input type="text" v-model="formInline.user" :placeholder="key">

                        </Input>
                    </FormItem>
                    <FormItem prop="code">
                        <Input style="width:68%" type="text" v-model="formInline.code" :placeholder="code">

                        </Input>
                        <input id="sendCode" @click="sendCode()" type="Button" :value="$t('uc.forget.sendcode')">

                        </input>
                    </FormItem>
                    <FormItem prop="password">
                        <Input type="password" v-model="formInline.password" :placeholder="$t('uc.forget.newpwd')">

                        </Input>
                    </FormItem>
                    <FormItem prop="repassword">
                        <Input type="password" v-model="formInline.repassword" :placeholder="$t('uc.forget.confirmpwd')">

                        </Input>
                    </FormItem>
                    <FormItem>
                        <Button style="width:100%;" type="info" @click="handleSubmit('formInline')">{{$t('uc.forget.save')}}</Button>
                    </FormItem>
                </Form>
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
                        callback(new Error(this.$t('uc.forget.pwdvalidate1')));
                    } else if (value !== this.formInline.password) {
                        callback(new Error(this.$t('uc.forget.pwdvalidate2')));
                    } else {
                        callback();
                    }
            };
            return {
              captchaObj:null,
              modal1:false,
              _captchaResult:null,
                buttonLists:[
                    {
                        "text":this.$t('uc.forget.resettelpwd')
                    },
                    {
                        "text":this.$t('uc.forget.resetemailpwd')
                    }
                ],
                changeActive:0,
                countdown:60,
                formInline: {
                    user: '',
                    code:'',
                    password: '',
                    repassword:''
                },
                ruleInline: {
                    user: [
                        { validator: validateUser, trigger: 'blur' }
                    ],
                    code: [
                        { required: true, message: '', trigger: 'blur' }
                    ],
                    password: [
                        { required: true, message: this.$t('uc.forget.newpwdtip'), trigger: 'blur' },
                        { type: 'string', min: 6, message: this.$t('uc.forget.pwdvalidate3'), trigger: 'blur' }
                    ],
                    repassword: [
                        { validator: validateRepassword, trigger: 'blur' },
                        { type: 'string', min: 6, message: this.$t('uc.forget.pwdvalidate3'), trigger: 'blur' }
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
　　　　　　 }
        },
        created:function(){
            this.init();
            this.actives(this.changeActive);
        },
        computed: {
          'isLogin': function() {
            return this.$store.getters.isLogin;
          },
        },
        methods: {
            init(){
              if (this.isLogin) {
                this.$router.push('/');
              }else {
                this.$store.state.HeaderActiveName='1-4';
              }
                // this.initGtCaptcha();
            },
            actives:function(index){
                this.changeActive=index;
                if(this.changeActive==0){
                    this.key=this.$t('uc.forget.telno');
                    this.code=this.$t('uc.forget.smscode');
                    this.ruleInline.user[0].message=this.$t('uc.forget.teltip');
                    this.ruleInline.code[0].message=this.$t('uc.forget.smscodetip');
                }else{
                    this.key=this.$t('uc.forget.email');
                    this.code=this.$t('uc.forget.emailcode');
                    this.ruleInline.user[0].message=this.$t('uc.forget.emailtip');
                    this.ruleInline.code[0].message=this.$t('uc.forget.emailcodetip');
                }
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
          afterValidate(){
            this.modal1 = false;
            if(this.changeActive==1){
              //发送邮件
              var params = {};
              params["account"] = this.formInline.user;
              params["geetest_challenge"] = this._captchaResult.geetest_challenge;//极验验证二次验证表单数据 chllenge
              params["geetest_validate"] = this._captchaResult.geetest_validate;//极验验证二次验证表单数据 validate
              params["geetest_seccode"] = this._captchaResult.geetest_seccode;//极验验证二次验证表单数据 seccode

              this.$http.post(this.host+'/uc/reset/email/code',params).then(response => {
                this.countdown=60;
                var resp=response.body;
                if(resp.code==0){
                  this.$Notice.success({
                    title: this.$t('common.tip'),
                    desc: resp.message
                  });
                }else{
                  this.$Notice.error({
                    title: this.$t('common.tip'),
                    desc: resp.message
                  });
                }
              });
            }else {
              var params = {};
              params["account"] = this.formInline.user;
              params["geetest_challenge"] = this._captchaResult.geetest_challenge;//极验验证二次验证表单数据 chllenge
              params["geetest_validate"] = this._captchaResult.geetest_validate;//极验验证二次验证表单数据 validate
              params["geetest_seccode"] = this._captchaResult.geetest_seccode;//极验验证二次验证表单数据 seccode
              this.$http.post(this.host+'/uc/mobile/reset/code',params).then(response => {
                this.countdown=60;
                var resp=response.body;
                if(resp.code==0){
                  this.$Notice.success({
                    title: this.$t('common.tip'),
                    desc: resp.message
                  });
                }else{
                  this.$Notice.error({
                    title: this.$t('common.tip'),
                    desc: resp.message
                  });
                }
              });
            }
          },
            handleSubmit(name) {
                this.$refs[name].validate((valid) => {
                    if (valid) {
                      if(this.changeActive==1){
                        var params = {};
                        params["account"] = this.formInline.user;
                        params["code"] = this.formInline.code;
                        params["mode"] = 1;
                        params["password"] = this.formInline.password;
                        this.$http.post(this.host+'/uc/reset/login/password',params).then(response => {
                          this.countdown=60;
                          var resp=response.body;
                          if(resp.code==0){
                            this.$Notice.success({
                              title: this.$t('common.tip'),
                              desc: resp.message
                            });
                            this.$router.push("/login");
                          }else{
                            this.$Notice.error({
                              title: this.$t('common.tip'),
                              desc: resp.message
                            });
                          }
                        });
                      }else {
                        var params = {};
                        params["account"] = this.formInline.user;
                        params["code"] = this.formInline.code;
                        params["mode"] = 0;
                        params["password"] = this.formInline.password;
                        this.$http.post(this.host+'/uc/reset/login/password',params).then(response => {
                          this.countdown=60;
                          var resp=response.body;
                          if(resp.code==0){
                            this.$Notice.success({
                              title: this.$t('common.tip'),
                              desc: resp.message
                            });
                            this.$router.push("/login");
                          }else{
                            this.$Notice.error({
                              title: this.$t('common.tip'),
                              desc: resp.message
                            });
                          }
                        });
                      }
                        // this.$Message.success(this.$t('uc.forget.resetpwdsuccess'));
                    } else {

                    }
                })
            },
            settime(){
                var obj=document.getElementById('sendCode');
                if(this.countdown == 0) {
                    obj.removeAttribute("disabled");
                    obj.value = this.$t('uc.forget.sendcode');
                    this.countdown = 60;
                    return;
                } else {
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
                        desc: this.ruleInline.user[0].message
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
        }
    }
</script>
