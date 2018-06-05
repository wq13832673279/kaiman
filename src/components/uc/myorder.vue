<template>
    <div class="nav-right">
        <div class="nav-right col-xs-12 col-md-10 padding-right-clear">
            <div class="bill_box rightarea padding-right-clear">
                <div class="order_box">
                    <Tabs value="name1" @on-click="showItem">
                        <TabPane :label="$t('uc.otcorder.unpaid')" name="name1">
                            <div class="order-table">
                                <Table :no-data-text="$t('common.nodata')" stripe :columns="tableColumnsOrder" :data="tableOrder" :loading="loading"></Table>
                                <div style="margin: 10px;overflow: hidden">
                                    <div style="float: right;">
                                        <Page v-if="totalPage > 0" :total="totalNum" :current="currentPage" show-total @on-change="changePage" :page-size="pageSize"></Page>
                                    </div>
                                </div>
                            </div>
                        </TabPane>
                        <TabPane :label="$t('uc.otcorder.paided')" name="name2">
                            <div class="order-table">
                                <Table :no-data-text="$t('common.nodata')" stripe :columns="tableColumnsOrder" :data="tableOrder" :loading="loading"></Table>
                                <div style="margin: 10px;overflow: hidden">
                                    <div style="float: right;">
                                        <Page v-if="totalPage > 0" :total="totalNum" :current="currentPage" show-total @on-change="changePage" :page-size="pageSize"></Page>
                                    </div>
                                </div>
                            </div>
                        </TabPane>
                        <TabPane :label="$t('uc.otcorder.finished')" name="name3">
                            <div class="order-table">
                                <Table :no-data-text="$t('common.nodata')" stripe :columns="tableColumnsOrder" :data="tableOrder" :loading="loading"></Table>
                                <div style="margin: 10px;overflow: hidden">
                                    <div style="float: right;">
                                        <Page v-if="totalPage > 0" :total="totalNum" :current="currentPage" show-total @on-change="changePage" :page-size="pageSize"></Page>
                                    </div>
                                </div>
                            </div>
                        </TabPane>
                        <TabPane :label="$t('uc.otcorder.canceled')" name="name0">
                            <div class="order-table">
                                <Table :no-data-text="$t('common.nodata')" stripe :columns="tableColumnsOrder" :data="tableOrder" :loading="loading"></Table>
                                <div style="margin: 10px;overflow: hidden">
                                    <div style="float: right;">
                                        <Page v-if="totalPage > 0" :total="totalNum" :pageSize="pageSize" show-total :current="currentPage" @on-change="changePage" ></Page>
                                    </div>
                                </div>
                            </div>
                        </TabPane>
                        <TabPane :label="$t('uc.otcorder.appealing')" name="name4">
                            <div class="order-table">
                                <Table :no-data-text="$t('common.nodata')" stripe :columns="tableColumnsOrder" :data="tableOrder" :loading="loading"></Table>
                                <div style="margin: 10px;overflow: hidden">
                                    <div style="float: right;">
                                        <Page v-if="totalPage > 0" :total="totalNum" :current="currentPage" show-total @on-change="changePage" :page-size="pageSize"></Page>
                                    </div>
                                </div>
                            </div>
                        </TabPane>
                        <Input v-model="ordKeyword" slot="extra" @on-change="handleSearch" icon="ios-search" :placeholder="$t('uc.otcorder.searchtip')" style="width: 250px;margin-right: 20px;"></Input>
                    </Tabs>
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
            ordKeyword: '',
            choseBtn: 0,
            whichItem: 1,
            tableOrder: [],
            loading: true,
            totalPage:0,
            pageSize: 10,
            totalNum:0,
            currentPage:1,
            loginmsg:this.$t('common.logintip'),
        }
    },
    methods: {
        // 获取历史记录信息
        handleListApproveHistory() {

        },
        changePage(pageNo) {
            if (pageNo > 0) pageNo = pageNo - 1;
            if (this.whichItem == 1) {
                this.getOrder(1, pageNo);
            } else if (this.whichItem == 2) {
                this.getOrder(2, pageNo);
            } else if (this.whichItem == 3) {
                this.getOrder(3, pageNo);
            } else if (this.whichItem == 0) {
                this.getOrder(0, pageNo);
            } else if (this.whichItem == 4) {
                this.getOrder(4, pageNo);
            }
        },
        getOrder(status, pageNo) {
            this.tableOrder = []
            let params = {}
            params['status'] = status
            params['pageNo'] = pageNo;
            params['pageSize'] = this.pageSize;
            this.currentPage = pageNo + 1;
            this.$http.post(this.host + '/otc/order/self', params).then(response => {
                var resp = response.body;
                if (resp.code == 0 && resp.data.content) {
                    this.tableOrder = resp.data.content;
                    this.totalPage = resp.data.totalPages;
                    this.totalNum = resp.data.totalElements;
                } else {
                    // this.$Message.error(resp.message);
                  // this.$Message.error(this.$t('common.logintip'));
                  this.$Message.error(this.loginmsg);
                }
                this.loading = false
            })
        },
        init() {
        },
        handleSearch() {
          this.tableOrder = []
          let params = {}
          params['status'] = this.whichItem;
          params['pageNo'] = 0;
          params['pageSize'] = this.pageSize;
          if(this.ordKeyword != "") {
            params['orderSn'] = this.ordKeyword;
          }
          this.currentPage = 1;
          this.$http.post(this.host + '/otc/order/self', params).then(response => {
            var resp = response.body;
            if (resp.code == 0 && resp.data.content) {
              this.tableOrder = resp.data.content;
              this.totalPage = resp.data.totalPages;
              this.totalNum = resp.data.totalElements;
            } else {
              this.$Message.error(resp.message);
            }
            this.loading = false
          })
        },
        showItem(name) {
            if (name == 'name1') {
                this.whichItem = 1
            } else if (name == 'name2') {
                this.whichItem = 2
            }
            else if (name == 'name3') {
                this.whichItem = 3
            }
            else if (name == 'name0') {
                this.whichItem = 0
            }
            else if (name == 'name4') {
                this.whichItem = 4
            }
            this.changePage(0);

        }

    },
    created() {
        this.changePage(0);
    },
    mounted() {
        // this.init();
    },
    computed: {
        tableColumnsOrder() {
            let self = this
            let columns = [];
            columns.push({
                title: this.$t('uc.otcorder.orderno'),
                key: 'orderSn',
                width: 155,
                render: function(h, params) {
                    return h('p', [
                        h('a', {
                            on: {
                                click: function() {
                                    self.$router.push('/chat?tradeId=' + params.row.orderSn);
                                }
                            }
                        }, params.row.orderSn),
                    ]);
                }
            });
            columns.push({
                title: this.$t('uc.otcorder.created'),
                key: 'createTime',
                width: 105,

            });
            columns.push({
                title: this.$t('uc.otcorder.symbol'),
                key: 'unit',
                width: 90,
            });
            columns.push({
                title: this.$t('uc.otcorder.type'),
                key: 'type',
                width: 90,
                render: (h, params) => {
                    let text = ''
                    if (params.row.type == 0) {
                        text = self.$t('uc.otcorder.type_buy');
                    } else {
                        text = self.$t('uc.otcorder.type_sell');
                    }
                    return h('div', [
                        h('p', text),
                    ]);
                }

            });
            columns.push({
                title: this.$t('uc.otcorder.tradename'),
                key: 'name',
                width: 155,
                render: function(h, params) {
                    return h('p', [
                        h('a', {
                            on: {
                                click: function() {
                                    self.$router.push('/checkuser?id=' + params.row.name);
                                }
                            }
                        }, params.row.name),
                    ]);
                }
            });
            columns.push({
                title: this.$t('uc.otcorder.amount'),
                key: 'amount',
            });
            columns.push({
                title: this.$t('uc.otcorder.money'),
                key: 'money',
            });
            columns.push({
                title: this.$t('uc.otcorder.fee'),
                key: 'commission',
            });

            return columns;
        },
    }
}
</script>
<style scoped>
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
    padding-top: 30px;
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
    text-align: left;
}

.order_box a {
    color: #0B0D1B;
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
