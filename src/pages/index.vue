<template>
    <div>
        <div id="fullpage">
            <div class="section" id="page1">
                <Carousel autoplay :arrow="showArrow" :autoplay-speed="speed" v-model="value2" loop>
                    <CarouselItem>
                        <div class="demo-carousel">
                            <div class="demo-carousel-btn">
                                <a class="purchase" @click="purchaseHref"></a>
                                <router-link class="register" to="/register"></router-link>
                            </div>
                        </div>
                    </CarouselItem>
                    <CarouselItem>
                        <div class="demo-carousel">
                            
                        </div>
                    </CarouselItem>
                </Carousel>
            </div>
            <div class="section" id="page2">
                <div class="ptjy">
                    <div class="usdt">
                        <div class="usdt_icon">
                            <img src="../../assets/images/usdt.png"></img>
                            <p>USDT2</p>
                        </div>
                        <ul>
                            <li :class="tab.class" v-for="tab in usdtList">
                                <router-link :to="tab.href">
                                    <span>{{tab.category}}</span>
                                    <label>{{tab.price}}</label>
                                    <label>
                                        {{tab.rate}}
                                    </label>
                                </router-link>
                            </li>
                        
                        </ul>
                    </div>
                    <div class="btc">
                        <div class="btc_icon">
                            <img src="../../assets/images/btc.png"></img>
                            <p>BTC</p>
                        </div>
                        <ul>
                            <li :class="tab.class" v-for="tab in btcList">
                                <router-link :to="tab.href">
                                    <span>{{tab.category}}</span>
                                    <label>{{tab.price}}</label>
                                    <label>
                                        {{tab.rate}}
                                    </label>
                                </router-link>
                            </li>
                        </ul>
                    </div>
                    <div class="eth">
                        <div class="eth_icon">
                            <img src="../../assets/images/eth.png"></img>
                            <p>ETH</p>
                        </div>
                        <ul>
                            <li :class="tab.class" v-for="tab in ethList">
                                <router-link :to="tab.href">
                                    <span>{{tab.category}}</span>
                                    <label>{{tab.price}}</label>
                                    <label>
                                        {{tab.rate}}
                                    </label>
                                </router-link>
                            </li>
                        </ul>
                    </div>
                </div>
            </div>
            <div class="section" id="page3">
                <label class="fadeinB">{{$t("sectionPage.ptaqTitle")}}</label>
                <p class="fadeinA">{{$t("sectionPage.ptaqContent")}}</p>
            </div>
            <div class="section" id="page4">
                <label class="fadeinB">{{$t("sectionPage.ptslTitle")}}</label>
                <p class="fadeinA">{{$t("sectionPage.ptslContent")}}</p>
            </div>
            <div class="section" id="page5">
                <div class="page5_title">{{$t("sectionPage.newsTitle")}}</div>
                <div class="page5_content">
                    <img style="float:left;width:30%;height:320px;" src="../../assets/images/news_left.png"></img>
                    <div style="float:left;width:40%;padding:0 75px;height:259px;">
                       <div class="news_title">COINBASE对BCC态度软化</div> 
                       <div class="news_date">2017-12-05</div>
                       <div class="news_detail">据VB报道，美国东部时间昨天，以太坊的交易量突破了40万，比比特币高出4万，创下虚拟货币新纪录。</div>
                       <img style="margin-top:190px;" src="../../assets/images/news_more.png"></img>
                    </div>
                    <img style="float:left;padding:5px 10px 0 0" src="../../assets/images/news_right.png"></img>
                    <ul>
                        <li :class="tab.class" v-for="tab in news">
                            <span>{{tab.date}}</span>
                            <label>{{tab.title}}</label>
                        </li>
                    </ul>
                </div>
            </div>
        </div>
        <div id="nav">
            <ul>
                <li><span>BANNER</span><a @click="goAnchor('#page1')"></a></li>
                <li><span>{{$t("nav.ptjy")}}</span><a @click="goAnchor('#page2')"></a></li>
                <li><span>{{$t("nav.ptaq")}}</span><a @click="goAnchor('#page3')"></a></li>
                <li><span>{{$t("nav.ptsl")}}</span><a @click="goAnchor('#page4')"></a></li>
                <li><span>{{$t("nav.xwzx")}}</span><a @click="goAnchor('#page5')"></a></li>
            </ul>
        </div>
    </div>
</template>
<style>
    #fullpage{
        background:#040417;
    }
    .section{
        height:640px;
        text-align:center;
        color:#fff;
    }
    .demo-carousel{
        background:url(../../assets/images/banner.png) no-repeat center;
        height:640px;
        background-size:cover;
    }
    .demo-carousel-btn{
        width:100%;
        height:100%;
        padding-top:345px;
    }
    .demo-carousel a{
        display:inline-block;
        width:250px;
        height:55px;
        margin:0 15px;
    }
    .purchase{
        background:url(../../assets/images/purchase.png) no-repeat;
    }
    .register{
        background:url(../../assets/images/register.png) no-repeat;
    }
    .ptjy{
        height:100%;
        margin:30px 10%;
    }
    .usdt{
        float:left;
        width:100%;
    }
    .usdt_icon{
        float:left;
        width:18%;
        height:290px;
        background:#1d293a;
        padding-top:125px;
        margin:5px;
    }
    .ptjy ul{
        float:left;
        width:80%;
    }
    .ptjy ul li{
        float:left;
        width:15%;
        height:140px;
        background:#1d293a;
        margin:5px;
        cursor:pointer;
    }
    .ptjy ul li a{
        color:#fff;
    }
    .ptjy ul li:hover{
        box-shadow:0 8px 16px rgba(29, 41, 255, 0.4)
    }
    .ptjy ul li.rise label{
        color:#32b114;
    }
    .ptjy ul li.drop label{
        color:#e01a1a;
    }
    .ptjy ul li span,.ptjy ul li label{
        display:block;
        padding:10px 0;
        cursor:pointer;
    }
    .ptjy ul li label img{
        vertical-align:middle;
    }
    
    .btc,.eth{
        float:left;
        width:100%;
        margin-top:10px;
    }
    .btc_icon,.eth_icon{
        float:left;
        width:18%;
        height:140px;
        background:#1d293a;
        padding-top:50px;
        margin:5px;
    }
    #nav{
        position:fixed;
        right:10%;
        top:50%;
        z-index:100;
    }
    #nav ul li {
        display: block;
        width: 120px;
        height: 25px;
        margin: 7px;
        position:relative;
        padding-right:20px;
        text-align:right;
        color:#fff;
    }
    #nav ul li span{
        display:none;
    }
    #nav ul li a{
        top: 2px;
        right: 2px;
        width: 8px;
        height: 8px;
        background:url(../../assets/images/page.png) no-repeat;
        position: absolute;
        z-index: 1;
    }
    #nav ul li a:hover,#nav ul li a.active{
        top: 0;
        right: -3px;
        width:18px;
        height:18px;
        background:url(../../assets/images/page_active.png) no-repeat;
        position: absolute;
        z-index: 1;
    }
    #page3{
        position:relative;
        color:#979797;
        background:url(../../assets/images/section3.png) no-repeat center;
    }
    #page3 label{
        position:absolute;
        top:30%;
        left:20%;
        font-size:30px;
    }
    @-webkit-keyframes fadeinB {
        0% {
            top:50% ;
            opacity:0;
            }
        100% {
            top:30%;
            opacity:1;
            } 
    }
    @keyframes fadeinB {
         0% {
            top:50% ;
            opacity:0;
            }
        100% {
            top:30%;
            opacity:1;
            } 
    }
    @-webkit-keyframes fadeinA {
        0% {
            top:60% ;
            opacity:0;
            }
        100% {
            top:40%;
            opacity:1;
            } 
    }
    @keyframes fadeinA {
        0% {
            top:60% ;
            opacity:0;
            }
        100% {
            top:40%;
            opacity:1;
            } 
    }
    #page3 p{
        position:absolute;
        top:40%;
        left:20%;
        font-size:15px;
    }
    #page4{
        position:relative;
        color:#979797;
        background:url(../../assets/images/section4.png) no-repeat center;
    }
    #page4 label{
        position:absolute;
        top:30%;
        left:70%;
        font-size:30px;
    }
    #page4 p{
        position:absolute;
        top:40%;
        left:70%;
        font-size:15px;
    }
    #page5{
        position:relative;
        color:#979797;
        background:url(../../assets/images/section5.png) no-repeat;
        padding:0 10%;
    }
    .page5_title{
        font-size:30px;
        line-height:200px;
    }
    .page5_content{
        text-align:left;    
    }
    .page5_content ul{
        float:left;
        width:27%;
    }
    .page5_content ul li{
        height:70px;
        overflow:hidden;
        text-overflow:ellipsis;
        white-space:nowrap;
    }
    .page5_content ul li span{
        margin-right:10px;
    }
    .news_1{
        color:#202b3c;
        font-size:12px;
    }
    .news_2{
        color:#505c6f;
        font-size:13px;
    }
    .news_3{
        color:#fff;
        font-size:18px;
    }
    .news_title{
        color:#fff;
        font-size:20px;
    }
    .news_date{
        color:#505c6f;
    }
    .news_detail{
        color:#98999f;
        margin-top:10px;
    }
</style>
<script>
var Stomp = require('stompjs');
var SockJS = require('sockjs-client');
var moment = require('moment');
var $=require('jquery');

export default {
    data(){
        return {
            value2:0,
            showArrow:'never',
            speed:5000,
            symbol:'',
            news:[
                {
                    class:'news_1',
                    date:'2017-12-05',
                    title:'比特币稀缺性超过黄金,成为今年最好的增值啊啊啊啊啊'
                },
                {
                    class:'news_2',
                    date:'2017-12-01',
                    title:'币行比特币新高23200 韩国立法监管或为推啊啊啊啊啊'
                },
                {
                    class:'news_3',
                    date:'2017-12-05',
                    title:'COINBASE对BCC态度软化'
                },
                {
                    class:'news_2',
                    date:'2017-11-20',
                    title:'阿鲁巴岛希望用以太坊促进旅游业发展啊啊啊啊啊'
                },
                {
                    class:'news_1',
                    date:'2017-11-13',
                    title:'加拿大央行成员发表文章,探讨央行发现加盟啊啊啊啊啊'
                }
            ],
            usdtList:[
                
            ],
            btcList:[
                
            ],
            ethList:[
                
            ]
        }
    },
    created:function(){
        this.init();
        this.getSymbol();
        require(["../../assets/js/index.js"],function(e){
            e.scrollFunction();
        });
    
    },
    mounted:function(){
            var stompClient = null;
            var that=this;

            var socket = new SockJS(that.$store.state.host1+'/market-ws');
            stompClient = Stomp.over(socket);
            stompClient.debug=false;
            stompClient.connect({}, function(frame) {
                stompClient.subscribe('/topic/market/thumb', function(msg) {
                    var resp = JSON.parse(msg.body);
                    //console.log(resp);
                    for(var i=0;i<that.usdtList.length;i++){
                        if(resp.symbol==that.usdtList[i].category){
                            that.usdtList[i].class= resp.change > 0 ? 'rise': 'drop'; 
                            that.usdtList[i].price=(resp.close).toFixed(2);
                            that.usdtList[i].rate=resp.chg>0 ? ('+'+(resp.chg*100).toFixed(2)+'%') : ((resp.chg*100).toFixed(2)+'%');
                        }
                    }

                });
            
            })
    },
    getAd(index) {
      if (index == 0) {
        this.$http.post(this.host + '/otc/advertise/excellent', { 'advertiseType': 0 }).then(response => {
          var resp = response.body;
          if (resp.code == 0) {
            this.cardListBuy0 = resp.data.slice(0, 4)
            console.log(resp.data)
          } else if (resp.code == 4000) {
            this.$Message.success('请先登录');
            this.$router.push('/login');
          } else {
            this.$Message.error(resp.message);
          }
        })
      } else if (index == 1) {
        this.$http.post(this.host + '/otc/advertise/excellent', { 'advertiseType': 1 }).then(response => {
          var resp = response.body;
          if (resp.code == 0) {
            this.cardListBuy1 = resp.data.slice(0, 4)
            console.log(resp.data)
          } else if (resp.code == 4000) {
            this.$Message.success('请先登录');
            this.$router.push('/login');
          } else {
            this.$Message.error(resp.message);
          }
        })
      }

    methods:{
        init(){
            this.$store.state.HeaderActiveName='1-1';
        },
        getSymbol(){
            this.$http.post(this.$store.state.host1+'/symbol-thumb',{}).then(response => {
                var resp=response.body;
                console.log(resp);
                for(var i=0;i<resp.length;i++){
                    var arr={};

                    arr.class= resp[i].change > 0 ? 'rise': 'drop'; 
                    
                    var a=(resp[i].symbol).toLowerCase().split('/')[0];
                    var b=(resp[i].symbol).toLowerCase().split('/')[1];
                    arr.href='/'+a+'_'+b+'/exchange';
                    arr.category=resp[i].symbol;
                    this.symbol=arr.category;
                    arr.price=(resp[i].close).toFixed(2);
                    arr.rate=resp[i].chg>0 ? ('+'+(resp[i].chg*100).toFixed(2)+'%') : ((resp[i].chg*100).toFixed(2)+'%');

                    this.usdtList.push(arr);
                }
                
            })
        },
        purchaseHref(){
            if(this.$store.state.showLogout==true){
                this.$router.push('login');
            }else{
                this.$router.push('tradingcenter/coin1buy');
            }
        },
        goAnchor(selector) {
            var anchor = this.$el.querySelector(selector);
            $('html,body').animate({scrollTop: anchor.offsetTop}, 1000);
            //document.documentElement.scrollTop = anchor.offsetTop;
        }
            
    }
    
}
</script>