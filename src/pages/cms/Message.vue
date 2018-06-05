<template>
    <div class="user_center" style="padding:20px 10%;">
        <Row type="flex">
            <Col span="5" class="layout_menu_left">
                <Menu active-name="1-1" theme="dark" width="auto" :open-names="['1']">
                    <Submenu name="1">
                        <router-link to="/message">
                            <MenuItem name="1-1">平台公告</MenuItem>
                        </router-link>
                        <router-link to="">
                            <MenuItem name="1-2">平台活动</MenuItem>
                        </router-link>
                        <router-link to="">
                            <MenuItem name="1-3">系统消息</MenuItem>
                        </router-link>
                        <router-link to="">
                            <MenuItem name="1-4">行业新闻</MenuItem>
                        </router-link>
                    </Submenu>
                </Menu>
            </Col>
            <Col span="18" class="layout_menu_right">
                <div class="aqzx">
                    <div class="menu_right_title">平台公告</div>
                    <div class="menu_right_content">
                        <ul>
                            <li>
                                <img src="../../assets/images/message_list.png">
                                <div class="message_list">
                                    <div class="message_title">CBOE将于12月10日开始比特币期货交易</div>
                                    <div class="message_content">该公司在12月4日发表的一份声明中表示，交易将于美国中部时间12月10日下午5点开始，
                                    周一（12月11日）将成为其第一个全天交易日。该产品将在CBOE期货交易所（CFE）进行交易，代号为"XBT"。该公司在其声明中补充道，
                                    这个期货产品的交易在12月底之前是免费的。</div>
                                </div>
                            </li>
                        </ul>
                    </div>
                </div>
            </Col>
        </Row>
    </div>
</template>
<style>
    .menu_right_content{
        margin:20px 30px;
    }
    .menu_right_content ul img{
        float:left;
        margin-right:20px;
    }
    .message_list{
        float:left;
        width:66%;
    }
    .message_title{
        height:40px;
        font-size:16px;
    }
    .message_content{
        line-height:25px;
        color:#979797;
    }
</style>
<script>
    export default {
        data(){
            return{
                
            }
        },
        created:function(){
            this.init();
        },
        methods:{
            init(){
                this.$store.state.HeaderActiveName='1-5';
            }
        }
    }
</script>
