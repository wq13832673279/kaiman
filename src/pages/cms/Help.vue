<template>
    <div class="help">
        <img src="../../assets/images/call.png">
        <div class="help_container">

            <Col span="7">
               <div>
                <img src="../../assets/images/consult.png">
                </div>
                 <router-link to="/notice">
                <h2>{{$t('cms.noticecenter')}}</h2>
                 </router-link>
                <!-- <a href="tencent://message/?uin=924499270&site=qq&menu=yes">

                </a> -->
            </Col>
            <Col span="7">
            <div>
                <img src="../../assets/images/help.png">
                </div>
                 <router-link to="/newhelp">
                <h2>{{$t('cms.newshelp')}}</h2>
                 </router-link>
            </Col>
            <Col span="7">
                <div>
                <img src="../../assets/images/userservice.png">
                </div>
                <h2  @click="showEwm">{{$t('cms.onlineservice')}}</h2>
            </Col>
            <div v-show="isShowWeChat" style="position: absolute;right: 66px;">
              <img src="../../assets/images/wechats.png">
            </div>
            <Col span="24" style="color:#000;font-size:18px;">
                <p style="line-height:50px;">{{$t('cms.faq')}}</p>
                <div v-for="item in FAQList" class="faqlist" >
                    <div class="fqtitle"><p>{{item.title}}<span style="margin-left: 20px;">{{item.createTime}}</span></p></div>
                    <div class="fqcontent" v-html="item.content"></div>
                </div>
            </Col>
        </div>
    </div>
</template>
<style>
.help {
  background: white;
  /* background:url(/assets/images/help_bg.png) no-repeat center; */
  height: 100%;
  background-size: cover;
  position: relative;
  overflow: hidden;
}
.help_container {
  padding: 0 12%;
  height: 100%;
}
.ivu-col-span-7 {
  text-align: center;
  background: #fff;
  border: 1px solid #ececec;
      padding: 47px 0;
  margin: 50px 2% 10px 2%;
  color: #000;
}
.ivu-col-span-7 div {
  background: #fff !important ;
}
.ivu-col-span-7 h2 {
  padding-top: 5px;
  line-height: 35px;
  font-size: 22px;
  font-weight: 500;
  color:#464650;
}
.ivu-col-span-7 p {
  font-size: 15px;
  line-height: 35px;
  padding-bottom: 15px;
}
.ivu-col-span-7 img {
  margin: 15px 0;
      height: 42px;
}
.ivu-col-span-7 button {
  width: 50%;
  margin: 10px 0;
  color: #000;
  background: #fff;
  font-size: 15px;
}
.ivu-col-span-7 button:hover {
  background: #464650;
}
.help_container .ivu-table th {
  text-align: center;
  background: #a3a3a3;
  color: #28313e;
  border: 0;
}
.help_container .ivu-table td {
  background: none;
  text-align: center;
  background: #7c7c7c;
  opacity: 0.5;
}
.help_container .ivu-table tr:last-child td {
  border: 0;
}
.faqlist{
text-align: left;

}
h2:hover{
cursor:pointer
}
.faqlist p{
    background: whitesmoke;
    line-height: 51px;
    padding:0 15px;
}
.faqlist div{
    color:#777;
    font-size: 14px;
    line-height:26px;
    padding:15px 15px;
    word-wrap: break-word;
}
</style>
<script>
export default {
  data() {
    return {
      isShowWeChat:false,
      FAQContent:'',
      FAQList: [],
    };
  },
  created: function() {
    this.init();
  },
  methods: {
    init() {
      this.$store.commit('navigate','nav-service');
      this.$store.state.HeaderActiveName = "1-7";

      this.loadFAQData();
    },
    loadFAQData(){
      let param = {};
      param["sysHelpClassification"] = 1;
      this.$http.post(this.host + "/uc/ancillary/system/help", param).then(response => {
        var resp = response.body;
        if(resp.code==0){
          this.FAQList = resp.data;
          // this.FAQContent = resp.data.content;
        }
      });
    }
    ,
    showEwm() {
      let onlinechatUrl = "http://kefu.caymanex.pro:80/im/text/15FwEk.html";
      window.open(onlinechatUrl);
      return ;
            // this.isShowWeChat = !this.isShowWeChat;
      const title = this.$t('common.tip');
      const content = '<p>'+this.$t('common.expect')+'</p>';
          this.$Modal.info({
            title: title,
            content: content,
            closable: true
          });
    },
  }
};
</script>
