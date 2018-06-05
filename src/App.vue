<template>
    <div class="page-view">
        <div class="page-content">
            <div class="layout">
                <div class="topnav">
                    <router-link to="/about-us">
                        {{topInfo.name}}
                    </router-link>
                </div>
                <div class="layout-ceiling">
                    <router-link to="/">
                        <div class="layout-logo"></div>
                    </router-link>
                    <div class="layout-ceiling-main">
                        <div class="header_nav">
                            <Menu :active-name="activeNav" theme="light" width="auto" :open-names="['1']">
                                <Submenu name="1">
                                    <router-link to="/">
                                        <MenuItem name="nav-index">{{$t("header.index")}}</MenuItem>
                                    </router-link>
                                    <router-link to="/otc/trade/usdt">
                                        <MenuItem name="nav-otc">{{$t("header.otc")}}</MenuItem>
                                    </router-link>
                                    <router-link to="/exchange">
                                        <MenuItem name="nav-exchange">{{$t("header.exchange")}}</MenuItem>
                                    </router-link>
                                    <router-link to="/finance">
                                        <MenuItem name="nav-asset">{{$t("header.asset")}}</MenuItem>
                                    </router-link>
                                    <router-link to="/uc/safe">
                                        <MenuItem name="nav-uc">{{$t("header.ucenter")}}</MenuItem>
                                    </router-link>
                                    <router-link to="/help">
                                        <MenuItem name="nav-service">{{$t("header.service")}}</MenuItem>
                                    </router-link>
                                </Submenu>
                            </Menu>
                        </div>
                        <div class="rr">
                            <div class="login_register" v-if="isLogin">
                                <Dropdown>
                                    <a href="javascript:void(0)">
                                        <Icon type="person" style="font-size: 20px;vertical-align: middle;"></Icon>
                                        <span>{{member.username}}</span>
                                        <Icon type="arrow-down-b"></Icon>
                                    </a>
                                    <DropdownMenu slot="list">
                                        <div @click="logout">
                                            <DropdownItem>
                                                <img src="./assets/images/logout.png"> {{$t("common.logout")}}
                                            </DropdownItem>
                                        </div>
                                    </DropdownMenu>
                                </Dropdown>
                            </div>
                            <div class="login_register" v-else>
                                <Menu active-name11="1-1" theme="light" width="auto" :open-names="['2']">
                                    <Submenu name="2">
                                        <router-link to="/login" id="login">
                                            <MenuItem name="1-1">{{$t("common.login")}}</MenuItem>
                                        </router-link>
                                        <router-link to="/register" id="register">
                                            <MenuItem name="1-2">{{$t("common.register")}}</MenuItem>
                                        </router-link>
                                    </Submenu>
                                </Menu>
                            </div>

                            <Dropdown @on-click="changelanguage">
                                <a style="width:90px;height:20px;line-height:20px;border:1px solid;border-radius:20px;padding:0 12px;" href="javascript:void(0)">
                                    {{languageValue}}
                                    <Icon type="arrow-down-b"></Icon>
                                </a>
                                <DropdownMenu slot="list">
                                    <DropdownItem v-if="languageValue=='简体中文'" name="en">English</DropdownItem>
                                    <DropdownItem v-else name="cn">简体中文</DropdownItem>
                                    <!--<DropdownItem name="hk">繁体中文</DropdownItem>-->
                                </DropdownMenu>
                            </Dropdown>
                        </div>
                    </div>
                </div>
            </div>
            <router-view></router-view>
            <div class="footer">
                <div class="footer_content">
                    <div class="footer_left">
                        <!--<img src="./assets/images/footer_logo.png"></img>-->
                        <h3>Caymanex.Pro</h3>
                        <p>{{$t("footer.gsmc")}}</p>
                        <p>Copyright © 2017 - 2018&nbsp;&nbsp;</p>
                    </div>
                    <div class="footer_right">
                        <ul>
                            <li class="footer_title">
                                <span>{{$t("footer.gsjj")}}</span>
                            </li>
                            <li>
                                <router-link to="/about-us">{{$t("footer.gywm")}}</router-link>
                            </li>
                            <li>
                                <router-link to="/join-us">{{$t("footer.jrwm")}}</router-link>
                            </li>
                        </ul>
                        <ul>
                            <li class="footer_title">
                                <span>{{$t("footer.bzzx")}}</span>
                            </li>
                            <li>
                                <!--<a href="#">{{$t("footer.xsrm")}}</a>-->
                              <router-link to="/newhelp/index?id=1">{{$t("footer.xsrm")}}</router-link>
                            </li>
                            <li>
                                <!--<a href="#">{{$t("footer.czzn")}}</a>-->
                              <router-link to="/newhelp/index?id=2">{{$t("footer.czzn")}}</router-link>
                            </li>
                            <li>
                                <!--<a href="#">{{$t("footer.jyzn")}}</a>-->
                              <router-link to="/newhelp/index?id=3">{{$t("footer.jyzn")}}</router-link>
                            </li>
                        </ul>
                        <ul>
                            <li class="footer_title">
                                <span>{{$t("footer.ptsm")}}</span>
                            </li>
                            <li>
                                <router-link to="/about-rule">{{$t("footer.fysm")}}</router-link>
                            </li>
                            <li>
                                <router-link to="/about-protocol">{{$t("footer.fwtk")}}</router-link>
                            </li>
                            <li>
                                <router-link to="/about-fee">{{$t("footer.fltk")}}</router-link>
                            </li>
                        </ul>
                      <ul>
                        <li class="footer_title">
                          <span>{{$t("footer.lxwm")}}</span>
                        </li>
                        <li>
                          <a href="javascript:;">kefu@caymanex.pro</a>
                        </li>
                        <li>
                          <a href="https://0.plus/Caymanofficial" target="_blank">币用</a><a href="http://t.me/Caymanofficial" target="_blank">telegram</a>
                        </li>
                      </ul>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import Vue from 'vue';
import { mapGetters, mapActions } from 'vuex';
export default {
    name: 'app',
    data() {
        return {
            topInfo:{name:'Cayman--领衔全球的数字资产交易平台',remark:'aaaa',createTime:'2018-01-10 11:37:27'}
            // languageValue: '简体中文'
        }
    },
    watch:{
      'activeNav':function () {
        switch (this.activeNav) {
          case "nav-exchange":
            break;
          default:
            window.document.title="领衔全球的数字资产交易平台 -- 【CAYMAN】";
            break;
        }
      }
    },
    computed: {
        'activeNav': function() {
            return this.$store.state.activeNav;
        },
        'isLogin': function() {
            return this.$store.getters.isLogin;
        },
        'member':function(){
            return this.$store.getters.member;
        },
        'languageValue':function () {
            var curlang = this.$store.getters.lang;
            if(curlang == "English") this.$i18n.locale = 'en';
            return curlang;
        }
    },
    created: function() {
        if (this.isMobileUserAgent()){
          location.href = "https://wap.caymanex.pro/";
          return;
        }
        var that = this;
        if ('-ms-scroll-limit' in document.documentElement.style && '-ms-ime-align' in document.documentElement.style) { // detect it's IE11
		  window.addEventListener("hashchange", function(event) {
		    var currentPath = window.location.hash.slice(1);
		    if (that.$router.path !== currentPath) {
		      that.$router.push(currentPath)
		    }
		  }, false)
		}
        this.initialize();
    },
    methods: {
        isMobileUserAgent:function(){
          return (/iphone|ipod|android|windows.*phone|blackberry.*mobile/i.test(window.navigator.userAgent.toLowerCase()));
        },
        initialize() {
            this.$store.commit('navigate','nav-index');
            this.$store.commit('recoveryMember');
            this.$store.commit('initLang');

            // this.loadTopInfo();
            this.checkLogin();
        },
        loadTopInfo(){ /*获取首页顶部公告*/
          let param = {};
          param["sysAdvertiseLocation"] = 2;
          this.$http.post(this.host + '/uc/ancillary/system/advertise', param).then(response => {
            var result = response.body;
            if(result.code == 0 && result.data.length > 0){
              this.topInfo = result.data[0];
            }
          });
        },
        logout() {
            this.$http.post(this.host + '/uc/logout', {}).then(response => {
                var resp = response.body;
                if (resp.code == 0) {
                    this.$Message.success(resp.message);
                    this.$store.commit('setMember',null);
                    location.href = "/";
                } else {
                    this.$Message.error(resp.message);
                }
            })
        },
        checkLogin() {
            this.$http.post(this.host + '/uc/check/login', {}).then(response => {
                var result = response.body;
                if(result.code == 0 && result.data == false){
                   this.$store.commit('setMember',null);
                }
            });
        },
        changelanguage: function(name) {
            if (name == 'en') {
                // this.languageValue = 'English';
                this.$store.commit('setlang','English');
                this.$i18n.locale = 'en';
            }
            if (name == 'cn') {
                // this.languageValue = '简体中文';
                this.$store.commit('setlang','简体中文');
                this.$i18n.locale = 'zh';
            }
            // if (name == 'hk') {
            //      this.languageValue = '繁体中文';
            // }
        }
    }
}
</script>

<style>
  #onlineservice{
    position: fixed;
    right: 20px;
    bottom: 40px;
    background: transparent;
}
  #onlineservice>a{
    background: transparent url("assets/images/onlineservice.jpg") no-repeat;
    display: block;
    /*width: 80px;*/
    /*height: 80px;*/
    width: 64px;
    height: 66px;
    background-size: cover;
    /*border-radius: 100%;*/
  }

/* top */
.ivu-select-selection .ivu-select-selected-value {
    color: #5f5f61;
}
.topnav {
    text-align: center;
    line-height: 25px;
    background: #1b262d;
}

.topnav a {
    color: #fff;
    font-size: 14px;
}

/*  */

.ivu-menu-light.ivu-menu-vertical .ivu-menu-item-active:not(.ivu-menu-submenu) {
    border-right: none;
}

.header_nav .ivu-menu-vertical.ivu-menu-light:after {
    width: 0;
}

.header_nav .ivu-menu-vertical .ivu-menu-item:hover,
.ivu-menu-vertical .ivu-menu-submenu-title:hover {
    background: none;
    color: #2d8cf0;
}
/*  */

html,
body {
    height: 100%;
    margin: 0;
    padding: 0;
    background: #263142;
    font-family: "Helvetica Neue", Helvetica, "PingFang SC", "Hiragino Sans GB", "Microsoft YaHei", "微软雅黑", Arial, sans-serif;
}

/*自定义滚动条样式*/

::-webkit-scrollbar {
    width: 10px;
    background: #0b0d1b;
}

::-webkit-scrollbar-thumb {
    background: #1f1b2a;
    border-radius: 25px;
}

.hide {
    display: none;
}

.blue {
    color: #6BF !important;
}

.red {
    color: #AE4E54 !important;
}









/* .ivu-input{
    background:#EAEDEE;
    border:0;
} */

.ivu-btn-info {
    background: #2AABFE;
    border-color: #2AABFE;
}

.ivu-btn-primary {
    /* background:#1855fd;
    border-color:#1855fd; */
}

.ivu-btn.active,
.ivu-btn:active {
    color: #fff;
    background: #2AABFE;
    border-color: #2AABFE;
}

.ivu-btn-text.active,
.ivu-btn-text:active {
    color: #2b85e4;
    background-color: transparent;
    border-color: transparent;
}

.ivu-btn.disabled,
.ivu-btn.disabled.active,
.ivu-btn.disabled:active,
.ivu-btn.disabled:focus,
.ivu-btn.disabled:hover,
.ivu-btn[disabled],
.ivu-btn[disabled].active,
.ivu-btn[disabled]:active,
.ivu-btn[disabled]:focus,
.ivu-btn[disabled]:hover,
fieldset[disabled] .ivu-btn,
fieldset[disabled] .ivu-btn.active,
fieldset[disabled] .ivu-btn:active,
fieldset[disabled] .ivu-btn:focus,
fieldset[disabled] .ivu-btn:hover {
    color: #fff;
    background: #54677F;
}

.ivu-carousel-dots li button {
    width: 30px;
    height: 10px;
    border-radius: 14px;
}

.ivu-menu-dark,
.ivu-menu-dark.ivu-menu-vertical .ivu-menu-opened {
    background: #18202A;
}

#checkbox {
    width: 10px;
}

#sendCode {
    position: absolute;
    border: 0;
    top: 0;
    right: 0;
    width: 30%;
    color: #D5851D;
    cursor: pointer;
}

.login_form {
    background: url(./assets/images/login_bg.jpg) no-repeat center;
    height: 760px;
    background-size: cover;
    position: relative;
    overflow: hidden;
}

.login_left {
    width: 50%;
    height: 400px;
    margin: 7% auto;
    background: #1E2125;
    position: relative;
    padding: 0 50px;
    color: #979797;
    font-size: 20px;
    margin-right: 2%;
}

.login_right {
    position: absolute;
    background: #fff;
    width: 350px;
    height: 510px;
    top: -55px;
    right: 50px;
}

.login_title {
    color: #000;
    text-align: center;
    height: 80px;
    font-size: 25px;
}









/* .login_right .ivu-select-selection{
        background:#EAEDEE;
} */

.login_right .ivu-select-dropdown {
    background: #fff;
}

.ivu-form-inline .ivu-form-item {
    display: block;
    margin-right: 0;
}









/* .user_center{
    padding:20px 10%;
}
.user_center .ivu-select-selection,.user_center .ivu-input{
    background:#263142;
    border:0;
    color:#fff;
}
.user_center .ivu-select-dropdown{
    background:#263142;
    color:#fff;
}
.user_center .ivu-select-item{
    color:#fff;
}
.user_center .ivu-select{
    color:#fff;
}
.user_center .ivu-select-item:hover,.user_center .ivu-select-item-selected,.user_center .ivu-select-item-selected:hover{
    background:#495060;
}
.user_center .ivu-table th{
        text-align:center;
        background:#28313E;
        color:#979797;
        border:0;
}
.user_center .ivu-table td{
        background:none;
        text-align:center;
        border-bottom:2px dashed #263142;
} */

.modify .ivu-input-wrapper {
    width: 40%;
}

.ivu-btn-ghost {
    /* color:#fff; */
}

.layout {
    position: relative;
}

.layout-logo {
    /*width: 100px;*/
    width:149px;
    height: 51px;
    background: url(./assets/images/logo.png) no-repeat;
    background-size: 100% 100%;
    float: left;
    position: relative;
}

.layout-copy {
    text-align: center;
    padding: 10px 0 20px;
    color: #9ea7b4;
}

.layout-ceiling {
    padding: 15px 6%;
    background: #fff;
    overflow: hidden;
}

.layout-ceiling-main {
    /* float: left; */
    height: 50px;
    line-height: 50px;
    margin-left: 150px;
}

.layout-ceiling-main .rr {
    float: right;
}

.layout-ceiling-main .ivu-menu-vertical .ivu-menu-item,
.ivu-menu-vertical .ivu-menu-submenu-title {
    padding: 0;
}

.layout-ceiling-main .ivu-menu-item {
    font-size: 14px;
}

.layout-ceiling-main a {
    color: #000;
    display: inline-block;
    line-height: 40px;
    height: 40px;
    text-align: center;
    margin-left: 30px;
    /*padding: 0 15px;*/
}

.header_nav {
    float: left;
    margin-right: 20px;
}

.header_nav .ivu-menu-dark.ivu-menu-vertical .ivu-menu-submenu .ivu-menu-item-active,
.header_nav .ivu-menu-dark.ivu-menu-vertical .ivu-menu-submenu .ivu-menu-item-active:hover {
    background: url(./assets/images/menu_active.png) !important;
}

.login_register .ivu-menu-dark.ivu-menu-vertical .ivu-menu-submenu .ivu-menu-item-active,
.login_register .ivu-menu-dark.ivu-menu-vertical .ivu-menu-submenu .ivu-menu-item-active:hover {
    background: #1855fd;
    border-radius: 5px;
}

.login_register {
    float: left;
}

#login.router-link-active,
#register.router-link-active{
    background: #27abe2;
    border-radius: 5px;
}
#login.router-link-active li,
#register.router-link-active li{
    color:#fff;
}
#login,
#register {
    color: #fff;
    display: inline-block;
    line-height: 25px;
    width: 75px;
    height: 25px;
    text-align: center;
    margin: 0;
}

.login_register a {
    margin-left: 0;
}

.ivu-dropdown-rel a {
    width: 100%;
}

.ivu-dropdown-menu {
    width: 100px;
}

.layout-ceiling-main .ivu-select-dropdown {
    background: #0b0d1b;
    margin-left: 25px;
}

.ivu-select-dropdown a {
    width: 100%;
    text-align: left;
    margin: 0;
}

.ivu-dropdown-item:hover {
    background: #aaa;
}

.ivu-dropdown-item {
    color: #fff;
}

.ivu-dropdown-item img {
    vertical-align: middle;
}

.ivu-radio-inner:after {
    background: #18202A;
}









/*安全中心*/

.user_center {
    height: 900px;
}

.ivu-menu-submenu-title {
    display: none;
}

.ivu-menu-item {
    text-align: center;
}

.ivu-menu-vertical .ivu-menu-submenu .ivu-menu-item {
    padding-left: 0 !important;
    padding-right: 0;
    color: #000;
    font-size: 16px;
    border-right: 0 !important;
}

.ivu-menu-dark.ivu-menu-vertical .ivu-menu-submenu .ivu-menu-item-active,
.ivu-menu-dark.ivu-menu-vertical .ivu-menu-submenu .ivu-menu-item-active:hover {
    background: #1855fd !important;
}

.rr .ivu-menu-vertical .ivu-menu-item:hover,
.ivu-menu-vertical .ivu-menu-submenu-title:hover {
    background: none;
    color: #2d8cf0;
}

.rr .ivu-menu-vertical.ivu-menu-light:after {
    width: 0;
}

.layout_menu_right {
    margin-left: 3%;
    background: #18202A;
    color: #fff;
    padding-bottom: 130px;
}

.menu_right_title {
    font-size: 16px;
    line-height: 45px;
    margin: 0 10px;
    padding-left: 20px;
    border-bottom: 1px solid #263142;
}









/* .ivu-form .ivu-form-item-label{
        color:#fff;
    }
    .ivu-form-item-required .ivu-form-item-label:before{
        display:none;
    } */

.category .ivu-radio-group.ivu-radio-group-button {
    width: 100%;
}

.category .ivu-radio-group label {
    font-size: 14px;
}

.category .ivu-radio-group-button .ivu-radio-wrapper {
    background: #28313E;
    color: #979797;
    border: 0;
    padding: 0 25px;
}

.category .ivu-radio-group-button .ivu-radio-wrapper-checked {
    color: #fff;
    background: #2F3D52;
    box-shadow: none;
}

.category .ivu-radio-wrapper span {
    padding-left: 0;
}

.purse_address_left {
    float: left;
    width: 86%;
}

.purse_address p {
    font-size: 10px;
    line-height: 25px;
    color: #979797;
}

.purse_address_left_icon {
    line-height: 40px;
    height: 40px;
    width: 100%;
}

.purse_address_left_icon img {
    vertical-align: middle;
    margin-right: 10px;
}

.purse_address span {
    font-size: 14px;
    float: left;
    color: #fff;
    padding: 0 20px;
    background: #28313E;
    width: 21%;
}

.purse_address_left_icon label {
    float: left;
    width: 72%;
    height: 40px;
    border: 2px solid #28313E;
    padding-left: 20px;
}

#qrcode canvas {
    width: 120px;
}

#qrcode img {
    width: 100%;
}

.ivu-select-item:hover {
    background: #aaa;
}

.ivu-select-item-selected,
.ivu-select-item-selected:hover {
    background: #aaa
}

.chart_container #chart_updated_time {
    float: left;
}

.footer {
    float: left;
    width: 100%;
}

.footer_content {
    height: 200px;
    padding: 50px 10%;
    color: #53575c;
    color:rgba(255,255,255,.8);
    background: #1b262d;
}

.footer_left {
    float: left;
    font-size: 14px;
}

.footer_left img {
    margin: 15px 0;
}

.footer_left p {
    margin: 10px 0;
    color:rgba(255,255,255,.6);
}

.footer_right {
    float: right;
    /*margin-top: 15px;*/
    text-align: center;
    /* margin-right: 20px; */
}

.footer_right ul {
    float: left;
    margin: 0 30px;
}

.footer_right ul li a {
    color: #53575c;
    color:rgba(255,255,255,.6);
    line-height: 25px;
    display: block;
}

.footer_title {
    font-size: 15px;
    height: 35px;
}

.ivu-select-selected-value {
    color: #bbbec4
}

/*法币交易*/

.ivu-col {
    text-align: center;
}
</style>
