<template>
    <div class="nav-right">
        <div class="nav-right col-xs-12 col-md-10 padding-right-clear">
            <div class="bill_box rightarea padding-right-clear record">
                <section class="trade-group merchant-top">
                    <i class="merchant-icon tips"></i>
                    <span class="tips-word">{{$t('uc.finance.withdraw.pickup')}}</span>
                    <span class="head-group">
                        <router-link to="/finance/withdraw/address">{{$t('uc.finance.withdraw.addressmanager')}}</router-link>
                    </span>
                </section>
                <section>
                    <div class="table-inner action-box">
                        <i class="angle" style="right: 27px;"></i>
                        <div class="action-inner">
                            <div class="inner-left">
                                <p class="describe">{{$t('uc.finance.withdraw.symbol')}}</p>
                                <Select v-model="coinType" style="width:100px;margin-top: 14px;" @on-change="getAddrList">
                                    <Option v-for="item in coinList" :value="item.unit" :key="item.unit">{{ item.unit }}</Option>
                                </Select>
                            </div>
                            <div class="inner-box">
                                <div class="form-group form-address">
                                    <label for="controlAddress" class="controlAddress describe">{{$t('uc.finance.withdraw.address')}}</label>
                                    <div class="control-input-group">
                                        <Select v-model="withdrawAdress">
                                            <Option v-for="item in currentCoin.addresses" :value="item.address" :key="item.address">{{ item.remark +'('+ item.address+')' }}</Option>
                                        </Select>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="form-group-container">
                            <div class="form-group form-amount">
                                <label class="label-amount"> {{$t('uc.finance.withdraw.num')}}
                                    <p class="label-fr">
                                        <span>【{{$t('uc.finance.withdraw.avabalance')}}】：
                                            <span class="label-pointer" id="valueAvailable">{{currentCoin.balance}}</span>
                                        </span>
                                        <span v-if="currentCoin.enableAutoWithdraw == 0">【{{$t('common.tip')}}】：{{$t('uc.finance.withdraw.msg1')}} {{currentCoin.threshold}} {{$t('uc.finance.withdraw.msg2')}}</span>
                                        <span>
                                            <a href="javascript:;" id="levelUp" style="display: none;">{{$t('uc.finance.withdraw.increase')}}</a>
                                        </span>
                                    </p>
                                </label>
                                <div class="input-group">
                                    <Poptip trigger="focus" :content="$t('uc.finance.withdraw.tip1')+currentCoin.withdrawScale+$t('uc.finance.withdraw.tip11')+currentCoin.minAmount+' ,'+$t('uc.finance.withdraw.tip2')+currentCoin.maxAmount" style="width: 100%;">
                                        <InputNumber @on-change="computerAmount" :precision="currentCoin.withdrawScale" v-model="withdrawAmount" :placeholder="$t('uc.finance.withdraw.numtip1')" size="large" style="width: 900px;"></InputNumber>
                                        <span class="input-group-addon addon-tag uppercase firstt">{{currentCoin.unit}}</span>
                                    </Poptip>

                                </div>
                            </div>
                        </div>
                        <div class="form-group-container form-group-container2">
                            <div class="form-group form-fee">
                                <label class="label-amount"> {{$t('uc.finance.withdraw.fee')}}
                                    <!--<p class="label-fr">-->
                                        <!--<span>{{$t('uc.finance.withdraw.range')}}：{{currentCoin.minTxFee}} - {{currentCoin.maxTxFee}}</span>-->
                                    <!--</p>-->
                                </label>
                                <div class="input-group">
                                    <Slider v-if="currentCoin.maxTxFee > currentCoin.minTxFee" v-model="withdrawFee"  show-input :step="(currentCoin.maxTxFee - currentCoin.minTxFee)/10" :max="currentCoin.maxTxFee" :min="currentCoin.minTxFee"></Slider>
                                    <!--<Poptip v-else trigger="focus" :content="$t('uc.finance.withdraw.tip1')+currentCoin.minTxFee+$t('uc.finance.withdraw.tip1')+currentCoin.maxTxFee" style="width: 100%;">-->
                                        <InputNumber readonly v-model="withdrawFee" :min="currentCoin.minTxFee" :max="currentCoin.maxTxFee" size="large" style="width: 440px;"></InputNumber>
                                        <span class="input-group-addon addon-tag uppercase" style="top: 32px;">{{currentCoin.unit}}</span>
                                    <!--</Poptip>-->
                                </div>
                            </div>
                            <div class="form-group">
                                <label>{{$t('uc.finance.withdraw.arriamount')}}</label>
                                <div class="input-group">
                                    <InputNumber readonly v-model="withdrawOutAmount" :placeholder="$t('uc.finance.withdraw.arriamount')" size="large" style="width: 100%;"></InputNumber>
                                    <!-- <input id="withdrawOutAmount" class="form-control form-out-amount" disabled="" maxlength="20" type="text" value="0"> -->
                                    <span class="input-group-addon addon-tag uppercase" style="top: 32px;">{{currentCoin.unit}}</span>
                                </div>
                            </div>
                        </div>
                        <div class="action-foot">
                            <Button id="withdrawSubmit" long size="large" type="primary" style="height:40px;" @click="apply">{{$t('uc.finance.withdraw.pickup')}}</Button>
                        </div>
                        <div class="action-content pt10">
                            <div class="action-body">
                                <p class="acb-p1">{{$t('common.tip')}}</p>
                                <p class="acb-p2">• {{$t('uc.finance.withdraw.msg3')}}：{{currentCoin.minAmount}}{{$t('uc.finance.withdraw.msg4')}}。<br>• {{$t('uc.finance.withdraw.msg5')}}<br>• {{$t('uc.finance.withdraw.msg6')}} </p>
                            </div>
                        </div>
                        <div class="action-content">
                            <div class="action-body">
                                <p class="acb-p1">{{$t('uc.finance.withdraw.record')}}</p>
                                <div class="order-table">
                                    <Table stripe :columns="tableColumnsWithdraw" :data="tableWithdraw" :loading="loading"></Table>
                                    <div style="margin: 10px;overflow: hidden">
                                        <div style="float: right;">
                                            <Page :total="transaction.total" :current="transaction.page + 1" @on-change="changePage"></Page>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </section>
            </div>
        </div>
      <Modal v-model="modal" :title="$t('otc.chat.tip')" @on-ok="ok">
        <P style="color:red;font-weight: bold;">
          {{$t('uc.finance.withdraw.fundpwdtip')}}<br/>
          <Input type="password" v-model="fundpwd" :placeholder="$t('otc.chat.msg7')"></Input>
        </p>
      </Modal>
    </div>
</template>
<script>

export default {
    data() {
        return {
            modal:false,
            fundpwd:'',
            currentCoin:{},
            transaction: {
                page:0,
                pageSize:10,
                total:0
            },
            loading: true,
            withdrawAdress: '',
            withdrawAmount: 0,
            withdrawFee: 0,
            withdrawOutAmount: 0,
            coinType: '',
            coinList: [],
            tableWithdraw: [],
            allTableWithdraw:[]
        }
    },
    watch:{
        currentCoin:function(){
            this.withdrawFee = this.currentCoin.minTxFee + (this.currentCoin.maxTxFee - this.currentCoin.minTxFee)/2;
        }
    },
    methods: {
        changePage() {
            this.getList(index -1)
        },
        getCurrentCoinRecharge() {
          if (this.coinType != "") {
            var temp = [];
            for (var i=0;i<this.allTableWithdraw.length;i++){
              if (this.allTableWithdraw[i].symbol == this.coinType) {
                temp.push(this.allTableWithdraw[i]);
              }
            }
            this.tableWithdraw = temp;
          }else {
            this.tableWithdraw = this.allTableWithdraw;
          }
        },
        ok(){
          if (this.fundpwd == "") {
            this.$Message.error(this.$t('otc.chat.msg7tip'));
            return;
          }
          let params = {}
          params['unit'] = this.currentCoin.unit
          params['address'] = this.withdrawAdress
          params['amount'] = this.withdrawAmount;
          params['fee'] = this.withdrawFee;
          params['jyPassword'] = this.fundpwd;
          this.$http.post(this.host + '/uc/withdraw/apply', params).then(response => {
            this.fundpwd = "";
            var resp = response.body;
            if (resp.code == 0) {
              this.getList();
              this.withdrawAmount = 0;
              this.$Message.success(resp.message);
            }else {
              this.$Message.error(resp.message);
            }
          });
        },
        getAddrList() {
            //获取地址
            this.$http.post(this.host + '/uc/withdraw/support/coin/info').then(response => {
                var resp = response.body;
                if (resp.code == 0 && resp.data.length > 0) {
                    this.coinList = resp.data;
                    if (this.coinType) {
                        for (let i = 0; i < resp.data.length; i++) {
                            if (this.coinType == resp.data[i].unit) {
                                this.currentCoin = resp.data[i];
                                break;
                            }
                        }
                    }
                    else{
                        this.currentCoin = this.coinList[0];
                        this.coinType = this.currentCoin.unit;
                    }
                } else {
                    this.$Message.error(resp.message);
                }
            })
            this.getCurrentCoinRecharge();
        },
        getList(pageNo) {
            //获取tableWithdraw
            let params = {}
            params['page'] = this.transaction.page
            params['pageSize'] = this.transaction.pageSize
            this.$http.post(this.host + '/uc/withdraw/record', params).then(response => {
                var resp = response.body;
                if (resp.code == 0) {
                    this.allTableWithdraw = resp.data.content;
                    this.getCurrentCoinRecharge();
                  //this.tableWithdraw = resp.data.content
                    this.transaction.total = resp.data.totalElements
                    this.transaction.page = resp.data.number
                    this.loading = false
                } else {
                    this.$Message.error(resp.message);
                }
            })
        },
        accSub(arg1, arg2) {
            var r1, r2, m, n;
            try { r1 = arg1.toString().split(".")[1].length } catch (e) { r1 = 0 }
            try { r2 = arg2.toString().split(".")[1].length } catch (e) { r2 = 0 }
            m = Math.pow(10, Math.max(r1, r2));
            //last modify by deeka
            //动态控制精度长度
            n = (r1 >= r2) ? r1 : r2;
            return ((arg1 * m - arg2 * m) / m).toFixed(n);
        },
        round(v, e) {
            var t = 1;
            for (; e > 0; t *= 10, e--);
            for (; e < 0; t /= 10, e++);
            return Math.round(v * t) / t;
        },
        computerAmount() {
          this.withdrawOutAmount = this.round(this.accSub(this.withdrawAmount, this.withdrawFee), this.currentCoin.withdrawScale)
        },
        computerAmount2() {
            this.withdrawAmount = (this.withdrawAmount + '').replace(/([0-9]+\.[0-9]{6})[0-9]*/, "$1") - 0
            this.withdrawOutAmount = this.round(this.accSub(this.withdrawAmount, this.withdrawFee), this.currentCoin.withdrawScale)
        },
        valid() {
            if (this.coinType == '') {
                this.$Message.error(this.$t('uc.finance.withdraw.symboltip'));
                return false
            } else if (this.withdrawAdress == '') {
                this.$Message.error(this.$t('uc.finance.withdraw.addresstip'));
                return false
            } else if (this.withdrawAmount == '' || this.withdrawAmount == 0 || (this.withdrawAmount - 0) < this.minAmount) {
                this.$Message.error(this.$t('uc.finance.withdraw.numtip2') + this.minAmount);
                return false
            } else if ((this.withdrawAmount - 0) < this.withdrawFee) {
                this.$Message.error(this.$t('uc.finance.withdraw.numtip3'));
                return false
            } else if (this.withdrawFee == '' || this.withdrawFee == 0 || (this.withdrawFee - 0) > this.currentCoin.maxTxFee || (this.withdrawFee - 0) < this.currentCoin.minTxFee) {
                this.$Message.error(this.$t('uc.finance.withdraw.feetip1') + this.currentCoin.minTxFee + ' , '+this.$t('uc.finance.withdraw.feetip2') + this.currentCoin.maxTxFee);
                return false
            } else {
                return true
            }
        },
        apply() {
            if (this.valid()) {


                this.modal = true;
                return;

            }

        },

    },
    created() {
        this.coinType = this.$route.query.name || "";
        this.getAddrList()
        this.getList(0, 10, 1)
    },
    computed: {
        tableColumnsWithdraw() {
            let columns = [];
            columns.push({
                title: this.$t('uc.finance.withdraw.time'),
                width: 180,
                key: 'createTime',
            });
            columns.push({
                title: this.$t('uc.finance.withdraw.symbol'),
                key: 'symbol',
                render:function(h,params){
                    return params.row.coin.unit;
                }
            });
            columns.push({
                title: this.$t('uc.finance.withdraw.address'),
                key: 'address',
            });
            columns.push({
                title: this.$t('uc.finance.withdraw.num'),
                key: 'totalAmount',
            });
            columns.push({
                title: this.$t('uc.finance.withdraw.fee'),
                key: 'fee',
            });
            columns.push({
                title: this.$t('uc.finance.withdraw.status'),
                key: 'status',
                render: (h, params) => {
                    let text = ''
                    if (params.row.status == 0) {
                        text = this.$t('uc.finance.withdraw.status_1');
                    } else if(params.row.status == 1){
                        text = this.$t('uc.finance.withdraw.status_2');
                    }
                    else if(params.row.status == 2){
                        text = this.$t('uc.finance.withdraw.status_3');
                    }
                    else if(params.row.status == 3){
                        text = this.$t('uc.finance.withdraw.status_4');
                    }
                    return h('div', [
                        h('p', text),
                    ]);
                }
            });
            return columns;
        }
    }
}
</script>
<style scoped>
.ivu-slider-button-wrap{
    top:-6px;
}
#withdrawAddressList {
    position: absolute;
    height: 0;
    transition: height .3s;
    top: 100%;
    left: 0;
    width: 100%;
    z-index: 1;
    max-height: 245px;
    overflow: auto;
    box-shadow: 0 3px 8px rgba(0, 0, 0, 0.1);
    height: auto;
    background: #fff;
}

#withdrawAddressList .address-item {
    padding: 0 20px;
    display: flex;
    line-height: 48px;
    border-bottom: 1px solid transparent;
    position: relative;
    white-space: nowrap;
    overflow: hidden;
    z-index: 99;
}

#withdrawAddressList .address-item:hover {
    background: #eee;
    cursor: pointer;
}

#withdrawAddressList .notes {
    position: absolute;
    bottom: 0;
    right: 20px;
    height: 48px;
    line-height: 48px;
    max-width: 300px;
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
}

p.describe {
    font-size: 16px;
    font-weight: 600;
}

.acb-p1 {
    font-size: 18px;
    font-weight: 600;
    line-height: 50px;
}

.acb-p2 {
    font-size: 14px;
    line-height: 24px;
}

.action-box {
    position: relative;
    text-align: left;
    border-radius: 3px;
    padding: 10px 20px 20px;
}

.action-content.pt10 {
    padding-top: 10px;
}

.action-content {
    width: 100%;
    margin-top: 20px;
    overflow: hidden;
    display: table;
}

.action-content .action-body {
    display: table-cell;
    vertical-align: top;
    line-height: 20px;
    font-size: 12px;
}

.action-foot {
    text-align: center;
    padding: 40px 170px 0;
}

.hb-night .btn.btn-primary,
.hb-night .btn.btn_submit {
    background-color: #7A98F7;
    color: white;
}

.action-inner {
    width: 100%;
    display: table;
}

.action-inner .inner-box {
    display: table-cell;
    width: 80%;
}

.form-group {
    position: relative;
    margin-bottom: 20px;
    font-size: 16px;
}

.hb-night .form-group label {
    color: #4E5B85;
}

.controlAddress {
    line-height: 50px;
}

.form-group label {
    max-width: 100%;
    /* display: inline-block; */
    /* font-size: 14px; */
    font-weight: 600;
}

.control-input-group {
    position: relative;
}

.control-input-group.open .select-list {
    height: auto;
}

.form-group-container {
    display: table;
    width: 100%;
}

.form-group-container .form-amount {
    width: 100%;
}

.form-group-container .form-group {
    display: table-cell;
}

.form-group-container .form-group span.addon-tag:last-child {
    padding: 0 20px;
    border: none;
    background: none;
    cursor: default;
    position: absolute;
    right: 20px;
    top: 8px;
}

.form-group-container .form-group span.addon-tag:last-child.firstt {
    top: 8px;
}

.form-group-container2 {
    padding-top: 20px;
}

.form-group-container .form-fee {
    width: 50%;
    padding: 0 20px 0 0;
}

.label-amount .label-fr {
    float: right;
    color: #aaa;
    font-size: 12px;
}

.label-amount .label-fr span {
    margin-left: 2px;
}

.form-group-container .form-group {
    display: table-cell;
}

.hb-night table.table .table-inner {
    margin: -4px -20px;
    position: relative;
    background-color: #181B2A;
    border-radius: 3px;
}

.hb-night table.table .table-inner {
    margin: -4px -20px;
    position: relative;
    background-color: #181B2A;
    border-radius: 3px;
}

.hb-night table.table .table-inner {
    margin: -4px -20px;
    position: relative;
    background-color: #181B2A;
    border-radius: 3px;
}

table.table .table-inner.action-box {
    margin: -1px -10px;
}

.merchant-top {
    height: 50px;
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-align: center;
    -ms-flex-align: center;
    align-items: center;
    background: #fff;
    padding: 0 15px;
    color: #0d214e;
}

.trade-group {
    margin-bottom: 20px;
    font-size: 14px;
}

.merchant-icon {
    display: inline-block;
    margin-left: 4px;
    background-size: 100% 100%;
}

.merchant-top .tips-word {
    -webkit-box-flex: 2;
    -ms-flex-positive: 2;
    flex-grow: 2;
    text-align: left;
}

.merchant-icon.tips {
    width: 4px;
    height: 22px;
    margin-right: 10px;
    background: #1755FD;
}

.bill_box {
    width: 100%;
    height: auto;
    overflow: hidden;
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

.rightarea .trade-process {
    line-height: 30px;
    padding: 0 15px;
    background: #f1f1f1;
    display: inline-block;
    position: relative;
    margin-right: 20px;
}

.rightarea .trade-process.active {
    color: #eb6f6c;
    background: #f9f5eb;
}

.rightarea .trade-process .icon {
    background: #fff;
    border-radius: 20px;
    height: 20px;
    width: 20px;
    display: inline-block;
    line-height: 20px;
    text-align: center;
    margin-right: 10px;
}

.rightarea .trade-process .arrow {
    position: absolute;
    top: 10px;
    right: -5px;
    width: 0;
    height: 0;
    border-top: 5px solid transparent;
    border-bottom: 5px solid transparent;
    border-left: 5px solid #f1f1f1;
}

.rightarea .trade-process.active .arrow {
    border-left: 5px solid #f9f5eb;
}

.rightarea .rightarea-tabs {
    border: none;
}

.rightarea .rightarea-tabs li>a {
    width: 100%;
    height: 100%;
    padding: 0;
    margin-right: 0;
    font-size: 14px;
    color: #646464;
    border-radius: 0;
    border: none;
    display: flex;
    justify-content: center;
    align-items: center;
}

.rightarea .rightarea-tabs li>a:hover {
    background-color: #fcfbfb;
}

.rightarea .rightarea-tabs li {
    width: 125px;
    height: 40px;
    position: relative;
    margin: -1px 0 0 -1px;
    border: 1px solid #f1f1f1;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
}

.rightarea .rightarea-tabs li.active {
    background-color: #fcfbfb;
}

.rightarea .rightarea-tabs li:last-child {
    border-right: 1px solid #f1f1f1;
}

.rightarea .rightarea-tabs li.active>a,
.rightarea .rightarea-tabs li:hover>a {
    color: #da2e22;
    border: none;
}

.rightarea .panel-tips {
    border: 3px solid #fdfaf3;
    color: #9e9e9e;
    font-size: 12px;
}

.rightarea .panel-tips .panel-header {
    background: #fdfaf3;
    line-height: 40px;
    margin-bottom: 15px;
}

.rightarea .panel-tips .panel-title {
    font-size: 16px;
}

.rightarea .recordtitle {
    cursor: pointer;
}

.nav-right {
    width: 1000px;
    height: auto;
    overflow: hidden;
    padding: 0 15px;
}

.order_box {
    width: 100%;
    background: #fff;
    height: 56px;
    line-height: 56px;
    margin-bottom: 20px;
    border-bottom: 2px solid #ccf2ff;
    position: relative;
    text-align: left;
}

.order_box a {
    color: #8994A3;
    font-size: 16px;
    padding: 0 30px;
    cursor: pointer;
    text-decoration: none;
    text-align: center;
    line-height: 54px;
    display: inline-block;
}

.order_box .active {
    border-bottom: 2px solid #00b5f6;
}

.order_box .search {
    position: absolute;
    width: 300px;
    height: 32px;
    top: 12px;
    right: 0;
    display: flex;
    /* border: #c5cdd7 solid 1px; */
}
</style>
