<template>
    <div class="nav-right">
        <div class="col-xs-12 col-md-10 padding-right-clear">
            <div style="text-align:left;margin:10px 0;">
                <Button icon="plus-round" type="primary" @click="publish">{{$t('otc.myad.post')}}</Button>
            </div>

            <Alert>{{$t('otc.myad.alert')}}</Alert>
            <div class="order-table">
                <Table stripe :columns="tableColumnsAdv" :data="tableAdv" :no-data-text="$t('common.nodata')" :loading="loading"></Table>
                <div style="margin: 10px;overflow: hidden">
                  <div style="float: right;">
                    <Page v-if="totalPage > 0" :pageSize="pageNumber" :total="totalPage" :current="currentPage" @on-change="changePage"></Page>
                  </div>
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
        let self = this;
        return {
            loginmsg:this.$t('common.logintip'),
            dataCount: 0,
            tableAdv: [],
            loading: true,
            tableColumnsAdv: [
                {
                    title: self.$t('otc.myad.no'),
                    key: 'id',
                },
                {
                    title: self.$t('otc.myad.type'),
                    key: 'advertiseType',
                    render: (h, params) => {
                        let text = ''
                        if (params.row.advertiseType == 0) {
                            text = self.$t('otc.myad.buy');
                        } else if (params.row.advertiseType == 1) {
                            text = self.$t('otc.myad.sell');
                        }
                        return h('div', [
                            h('p', text),
                        ]);
                    }
                },
                {
                    title: self.$t('otc.myad.limit'),
                    key: 'limit',
                    render: (h, params) => {
                        return h('div', [
                            h('p', params.row.minLimit + '~' + params.row.maxLimit),
                        ]);
                    }
                },
                {
                    title: self.$t('otc.myad.remain'),
                    key: 'remainAmount',
                },
                {
                    title: self.$t('otc.myad.coin'),
                    key: 'coinUnit',
                },
                {
                    title: self.$t('otc.myad.created'),
                    key: 'createTime',
                    width: 160,
                },
                {
                    title: self.$t('otc.myad.operate'),
                    key: 'buyBtn',
                    width: '180',
                    render: function(h, params) {
                        return h('p', [
                            h('a', {
                                on: {
                                    click: function() {
                                        if (params.row.status == 0) {
                                            self.$Message.error(self.$t('otc.myad.errmsg'));
                                        } else {
                                            self.$router.push('/otc/ad/update?id=' + params.row.id);
                                        }

                                    }
                                }

                            }, [
                                    h('Button', {
                                        props: {
                                            type: 'ghost',
                                            size: 'small'
                                        },
                                        style: {
                                            marginRight: '8px',
                                        },
                                    }, self.$t('otc.myad.update')),
                                ]),
                            h('Button', {
                                props: {
                                    type: 'primary',
                                    size: 'small'
                                },
                                style: {
                                    marginRight: '8px',
                                },
                                on: {
                                    click: () => {
                                        //要上架
                                        if (params.row.status == 1) {
                                            let canshu = {};
                                            canshu['id'] = params.row.id
                                            // canshu['status'] = params.row.status == 0 ? 1 : 0
                                            self.$http.post(self.host + '/otc/advertise/on/shelves', canshu).then(response => {
                                                var resp = response.body;
                                                if (resp.code == 0) {
                                                    self.$Message.success(resp.message);
                                                    // self.$router.go(0)
                                                    self.getAd()
                                                } else {
                                                    self.$Message.error(resp.message);
                                                }
                                            })
                                        } else if (params.row.status == 0) {
                                            let canshu = {};
                                            canshu['id'] = params.row.id
                                            // canshu['status'] = params.row.status == 0 ? 1 : 0
                                            self.$http.post(self.host + '/otc/advertise/off/shelves', canshu).then(response => {
                                                var resp = response.body;
                                                if (resp.code == 0) {
                                                    self.$Message.success(resp.message);
                                                    // self.$router.go(0)
                                                    self.getAd()
                                                } else {
                                                    self.$Message.error(resp.message);
                                                }
                                            })
                                        }

                                    }
                                }
                            }, params.row.status == 0 ? self.$t('otc.myad.dropoff') : self.$t('otc.myad.shelf')),
                            h('Button', {
                                props: {
                                    type: 'error',
                                    size: 'small'
                                },
                                on: {
                                    click: () => {
                                        let canshu = {};
                                        canshu['id'] = params.row.id

                                        if (params.row.status == 1) {
                                          self.$Modal.confirm({
                                            title: self.$t('common.tip'),
                                            content: '<p>'+self.$t('common.delete')+'</p>',
                                            onOk: () => {
                                              self.$http.post(self.host + '/otc/advertise/delete', canshu).then(response => {
                                                var resp = response.body;
                                                if (resp.code == 0) {
                                                  self.$Message.success(resp.message);
                                                  self.remove(params.index)
                                                } else {
                                                  self.$Message.error(resp.message);
                                                }
                                              })
                                            }
                                          });
                                        }else {
                                          self.$Message.error("下架广告后才可以删除！");
                                        }
                                    }
                                }
                            }, self.$t('otc.myad.delete'))
                        ]);
                    }
                },
            ],
            totalPage:0,
            pageNumber:10,
            currentPage:1
        }
    },
    methods: {
      updateLangData(){
        this.tableColumnsAdv[0].title = this.$t("otc.myad.no");
        this.tableColumnsAdv[1].title = this.$t("otc.myad.type");
        this.tableColumnsAdv[2].title = this.$t("otc.myad.limit");
        this.tableColumnsAdv[3].title = this.$t("otc.myad.remain");
        this.tableColumnsAdv[4].title = this.$t("otc.myad.coin");
        this.tableColumnsAdv[5].title = this.$t("otc.myad.created");
        this.tableColumnsAdv[6].title = this.$t("otc.myad.operate");
      },
        remove(index) {
            this.tableAdv.splice(index, 1);
        },
        changePage() {

        },
        getAd() {
            //获取个人广告
            this.$http.post(this.host + '/otc/advertise/all').then(response => {
                var resp = response.body;
                if (resp.code == 0) {
                    this.tableAdv = resp.data;
                    this.loading = false
                    this.dataCount = resp.data.length
                } else {
                    // this.$Message.error(resp.message);
                    // this.$Message.error(this.$t('common.logintip'));
                  this.$Message.error(this.loginmsg);
                }
            })
        },
        publish(){
            this.$router.push(this.api.otc.createAd);
        }

    },
    computed: {
        'lang': function () {
          return this.$store.state.lang;
        }
    },
    watch:{
      'lang':function () {
        this.updateLangData();
      }
    }
    ,
    created() {
        this.getAd()
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
    padding-top: 20px;
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
