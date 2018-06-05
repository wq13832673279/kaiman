<style scoped>
    .expand-row{
        margin-bottom: 16px;
    }
</style>
<template>
    <div>
        <Row class="expand-row">
            <Col span="6">
                <span class="expand-key">{{$t('exchange.expand.time')}} </span>
            </Col>
            <Col span="6">
                <span class="expand-key">{{$t('exchange.expand.price')}} </span>
            </Col>
            <Col span="6">
                <span class="expand-key">{{$t('exchange.expand.amount')}} </span>
            </Col>
            <Col span="6">
                <span class="expand-key">{{$t('exchange.expand.fee')}}</span>
            </Col>
        </Row>
        <Row v-for="row in rows">
            <Col span="6">
                <span class="expand-value">{{ row.time|dateFormat }}</span>
            </Col>
            <Col span="6">
                <span class="expand-value">{{ row.price }}</span>
            </Col>
            <Col span="6">
                <span class="expand-value">{{ row.amount }}</span>
            </Col>
            <Col span="6">
                <span class="expand-value">{{ row.fee }}</span>
            </Col>
        </Row>
    </div>
</template>
<script>
    export default {
        props: {
            rows: Array
        }
    };
</script>
