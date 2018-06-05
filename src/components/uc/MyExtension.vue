<template>
    <div class="nav-right">
        <div class="nav-right col-xs-12 col-md-10 padding-right-clear">
            <div class="bill_box rightarea padding-right-clear record account-box">
              <ButtonGroup>
                <Button v-for="(list,index) in buttonLists" :key="list.text" class="btStyle" :class="{active:changeActive == index}" @click="actives(index)">{{list.text}}</Button>
              </ButtonGroup>
                <div class="message" v-if="this.changeActive==0">
                    <p class="tips">{{$t('uc.extension.linkdesc')}}</p>
                    <div class="inner-box deposit-address">
                        <p class="describe">{{$t('uc.extension.linktitle')}}</p>
                        <div class="title">
                            <Input v-model="qrcode.value" readonly style="width: 600px" size="large"></Input>
                            <a v-clipboard:copy="qrcode.value" v-clipboard:success="onCopy" v-clipboard:error="onError" href="javascript:;" id="copyBtn" class="link-copy"><Button type="primary" style="width:120px">{{$t('uc.extension.copy')}}</Button></a>
                        </div>
                    </div>
                </div>
                <div class="message" v-else-if="this.changeActive==1">
                    <Table stripe :columns="tablePromoteFriends" :data="dataPromoteFriends" :loading="loading"></Table>
                </div>
                <div class="message" v-else>
                  <Table stripe :columns="tablePromoteMoney" :data="dataPromoteMoney" :loading="loading"></Table>
                    <!--<Col span="12" class="commission">-->
                        <!--<p>{{$t('uc.extension.currcommission')}}：<span><strong>{{currentCommission}}</strong>{{$t('uc.extension.yuan')}}</span></p>-->
                    <!--</Col>-->
                    <!--<Col span="12" class="commission">-->
                        <!--<p>{{$t('uc.extension.currcommission')}}：<span>{{$t('uc.extension.managerfee')}}<strong>{{commissionPaying}}</strong></span></p>-->
                    <!--</Col>-->
                </div>
            </div>
        </div>
    </div>
</template>
<script>

export default {
    components: {
    },
    data() {
        return {
            buttonLists:[
                {
                    "text":this.$t('uc.extension.title1')
                },
                {
                    "text":this.$t('uc.extension.title2')
                },
                {
                    "text":this.$t('uc.extension.title3')
                }
            ],
            currentCommission:'0.00',
            commissionPaying:'6%',
            changeActive:0,
            qrcode: {
                value: '',
                size: 200,
            },
            loading: true,
            tablePromoteFriends:[
                {
                    title: this.$t('uc.extension.username'),
                    key: 'username',
                    align: 'center',
                },
                {
                    title: this.$t('uc.extension.createdtime'),
                    key: 'createTime',
                    align: 'center',
                },
                {
                  title:this.$t('uc.extension.userlevel'),
                  key:'level',
                  align:'center',
                  render:function(h,params){
                    return (parseInt(params.row.level)+1)+"级";
                  }
                }
            ],
            dataPromoteFriends:[],
            tablePromoteMoney:[
                {
                  title:this.$t('uc.extension.symbol'),
                  key:'symbol',
                  align:'center'
                },
                {
                  title:this.$t('uc.extension.amount'),
                  key:'amount',
                  align:'center',
                },
                {
                  title:this.$t('uc.extension.amounttime'),
                  key:'createTime',
                  align:'center'
                },
                {
                  title:this.$t('uc.extension.remark'),
                  key:'remark',
                  align:'center'
                }
            ],
            dataPromoteMoney:[],
        }
    },
    methods: {
        getList() {
            this.loading=false;
        },
        actives(index){
            this.changeActive=index;
        },
        qrcodeM(){
            var promotionCode = this.user.promotionCode;
            this.qrcode.value="https://www.caymanex.pro/#/register?agent="+promotionCode;
        },
        onCopy(e) {
            this.$Message.success(this.$t('uc.extension.copy_msg1') + e.text);
        },
        onError(e) {
            this.$Message.error(this.$t('uc.extension.copy_msg2'));
        },
        getPromotionList(){
          this.$http.post(this.host + '/uc/promotion/record', {}).then(response => {
            var resp = response.body;
            if (resp.code == 0) {
              this.dataPromoteFriends = resp.data;
            } else {
              // this.$Message.error(resp.message);
            }
          })
        },
        getPromotionMoney(){
          this.$http.post(this.host + '/uc/promotion/reward/record', {}).then(response => {
            var resp = response.body;
            if (resp.code == 0) {
                this.dataPromoteMoney = resp.data;
            } else {
              // this.$Message.error(resp.message);
            }
          })
        }
    },
    created() {
        this.actives(this.changeActive);
        this.qrcodeM();
        this.getList();
        this.getPromotionList();
        this.getPromotionMoney();
    },
    computed: {
      user: function() {
        return JSON.parse(localStorage.getItem("MEMBER"))
      },
    }
}
</script>
<style scoped>
.nav-right {
    width: 1000px;
    height: auto;
    overflow: hidden;
    padding: 0 15px;
}
.nav-right .btStyle{
    width: 174px;
    height: 42px;
    font-size: 1.125em;
    color: #a2a0a1;
    background:#fff;
    margin: 50px 0;
}
.nav-right .active{
    background: #49a6f6;
    color: #fff;
}
.rightarea .message{
    width:96%;
    margin:0 auto;
    font-size:16px;
    color:#636363;
    padding-bottom:140px;
}
.nav-right .message .tips{
    text-align:left;
    padding-bottom:50px;
    border-bottom:1px dashed #e9e9e9;
}
.rightarea {
    background: #fff;
    padding-left: 15px !important;
    padding-right: 15px !important;
    margin-bottom: 60px !important;
}

.rightarea .rightarea-top {
    line-height: 75px;
    border-bottom: #f1f1f1 solid 1px;
}

.rightarea .rightarea-con {
    padding-top: 30px;
    padding-bottom: 125px;
}
.message .title .copy {
    user-select: text;
}
.message .title {
    float:left;
    margin:46px 0 0px 0;
}
.message .inner-box {
    display: table-cell;
    width: 100%;
}
.message a.link-copy {
    margin-left: 10px;
}
.message .describe{
    float:left;
    margin:52px 36px 0 0;
}
.message .commission{
    padding-bottom:50px;
    border-bottom:1px dashed #e9e9e9;
}
.message .commission span{
    color:#ff3533;
}
.message .commission strong{
    font-size:26px;
}
</style>
