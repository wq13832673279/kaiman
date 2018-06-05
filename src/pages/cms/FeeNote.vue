<template>
  <div class="agreement">
    <img src="../../assets/images/call.png">
    <div class="agreement_tab">
      <div class="static_main">
        <router-link to="/about-rule">{{$t('cms.exchangerule')}}</router-link>
        <router-link to="/about-protocol">{{$t('cms.useprotocol')}}</router-link>
        <router-link to="/about-fee" class="cur">{{$t('cms.feenote')}}</router-link>
        <router-link to="/about-merchant">{{$t('cms.merchantprocotol')}}</router-link>
      </div>
    </div>
    <div class="content">
      <div class="agreen-cont ">

        <div class=WordSection1 style='layout-grid:15.6pt'>

          <p class=MsoNormal><span lang=EN-US style='font-family:宋体;color:black'>2018.03.28-2018.04.30
Cayman</span><span style='font-family:宋体;color:black'>平台交易手续费限时优惠</span></p>

          <p class=MsoNormal align=left style='text-align:left'><b><span
            style='font-family:宋体'>一、法币交易</span></b><b><span style='font-family:宋体'>费率</span></b></p>

          <p class=MsoNormal align=left style='text-align:left'><span lang=EN-US
                                                                      style='font-family:宋体'>1</span><span style='font-family:宋体'>、法币交易区买入和卖出数字资产</span><span
            style='font-family:宋体;background:white'>手续费全免；</span></p>

          <p class=MsoNormal align=left style='text-align:left'><span lang=EN-US
                                                                      style='font-family:宋体'>2</span><span style='font-family:宋体'>、法币交易区发布广告完成交易收取广告方交易额的<span
            lang=EN-US>0.5%</span>作为手续费。</span></p>

          <p class=MsoNormal align=left style='text-align:left'><b><span lang=EN-US
                                                                         style='font-family:宋体'>&nbsp;</span></b></p>

          <p class=MsoNormal align=left style='text-align:left;'><b><span lang=EN-US style='font-family:宋体'>二、</span></b><b><span
            style='font-family:宋体'>币币交易费率</span></b></p>

          <!--<p class=MsoNormal align=left style='text-align:left;background:white'><span-->
            <!--lang=EN-US style='font-family:宋体;background:white'>1</span><span-->
            <!--style='font-family:宋体;background:white'>、币币交易（不含<span lang=EN-US>GCX)</span>手续费全免；</span></p>-->

          <!--<p class=MsoNormal align=left style='text-align:left;background:white'><span-->
            <!--lang=EN-US style='font-family:宋体;background:white'>2</span><span-->
            <!--style='font-family:宋体;background:white'>、<span lang=EN-US>GCX</span>交易手续费<span-->
            <!--lang=EN-US>1%</span>；</span></p>-->

          <table class=MsoNormalTable border=1 cellspacing=0 cellpadding=0 align=left
                 width=0 style='background:white;border-collapse:collapse;border:none;'>
            <tr style='height:18.45pt'>
              <td width=131 style='width:98.0pt;border:dotted windowtext 1.0pt;padding:
  0cm 18.0pt 0cm 18.0pt;height:18.45pt'>
                <span lang=EN-US style='font-family:宋体;color:black'>&nbsp;</span>
              </td>
              <td width=200 style='width:149.9pt;border:dotted windowtext 1.0pt;border-left:
  none;padding:0cm 18.0pt 0cm 18.0pt;height:18.45pt'>
                  <span style='font-family:宋体;color:black'>挂单</span>
              </td>
              <td width=239 style='width:179.35pt;border:dotted windowtext 1.0pt;
  border-left:none;padding:0cm 18.0pt 0cm 18.0pt;height:18.45pt'>
                <span style='font-family:宋体;color:black'>吃单</span>
              </td>
            </tr>
            <tr style="height: 18.45pt" v-for="(item,index) in symbol">
              <td width=131 style='width:98.0pt;border:dotted windowtext 1.0pt;border-top:none;padding:0cm 18.0pt 0cm 18.0pt;height:18.45pt'>
                  <span lang=EN-US style='font-family:宋体;color:black'>{{item.symbol}}</span>
              </td>
              <td width=200 style='width:149.9pt;border-top:none;border-left:none;
  border-bottom:dotted windowtext 1.0pt;border-right:dotted windowtext 1.0pt;
  padding:0cm 18.0pt 0cm 18.0pt;height:18.45pt'>
                  <span lang=EN-US style='font-family:宋体;color:black'>{{parseFloat(item.fee*100) + "%"}}</span>
              </td>
              <td width=239 style='width:179.35pt;border-top:none;border-left:none;
  border-bottom:dotted windowtext 1.0pt;border-right:dotted windowtext 1.0pt;
  padding:0cm 18.0pt 0cm 18.0pt;height:18.45pt'>
                  <span lang=EN-US style='font-family:宋体;color:black'>{{parseFloat(item.fee*100) + "%"}}</span>
              </td>
            </tr>
            <!--<tr style='height:18.45pt'>-->
              <!--<td width=131 style='width:98.0pt;border:dotted windowtext 1.0pt;border-top:-->
  <!--none;padding:0cm 18.0pt 0cm 18.0pt;height:18.45pt'>-->
                <!--<p class=MsoNormal align=center style='text-align:center'><span lang=EN-US-->
                                                                                <!--style='font-family:宋体;color:black'>BTC/</span><span lang=EN-US-->
                                                                                                                                    <!--style='font-family:宋体;color:black'>USDT</span></p>-->
              <!--</td>-->
              <!--<td width=200 style='width:149.9pt;border-top:none;border-left:none;-->
  <!--border-bottom:dotted windowtext 1.0pt;border-right:dotted windowtext 1.0pt;-->
  <!--padding:0cm 18.0pt 0cm 18.0pt;height:18.45pt'>-->
                <!--<p class=MsoNormal align=center style='text-align:center'><span lang=EN-US-->
                                                                                <!--style='font-family:宋体;color:black'>0%</span></p>-->
              <!--</td>-->
              <!--<td width=239 style='width:179.35pt;border-top:none;border-left:none;-->
  <!--border-bottom:dotted windowtext 1.0pt;border-right:dotted windowtext 1.0pt;-->
  <!--padding:0cm 18.0pt 0cm 18.0pt;height:18.45pt'>-->
                <!--<p class=MsoNormal align=center style='text-align:center'><span lang=EN-US-->
                                                                                <!--style='font-family:宋体;color:black'>0%</span></p>-->
              <!--</td>-->
            <!--</tr>-->
            <!--<tr style='height:18.45pt'>-->
              <!--<td width=131 style='width:98.0pt;border:dotted windowtext 1.0pt;border-top:-->
  <!--none;padding:0cm 18.0pt 0cm 18.0pt;height:18.45pt'>-->
                <!--<p class=MsoNormal align=center style='text-align:center'><span lang=EN-US-->
                                                                                <!--style='font-family:宋体;color:black'>BCH/</span><span lang=EN-US-->
                                                                                                                                    <!--style='font-family:宋体;color:black'>USDT</span></p>-->
              <!--</td>-->
              <!--<td width=200 style='width:149.9pt;border-top:none;border-left:none;-->
  <!--border-bottom:dotted windowtext 1.0pt;border-right:dotted windowtext 1.0pt;-->
  <!--padding:0cm 18.0pt 0cm 18.0pt;height:18.45pt'>-->
                <!--<p class=MsoNormal align=center style='text-align:center'><span lang=EN-US-->
                                                                                <!--style='font-family:宋体;color:black'>0%</span></p>-->
              <!--</td>-->
              <!--<td width=239 style='width:179.35pt;border-top:none;border-left:none;-->
  <!--border-bottom:dotted windowtext 1.0pt;border-right:dotted windowtext 1.0pt;-->
  <!--padding:0cm 18.0pt 0cm 18.0pt;height:18.45pt'>-->
                <!--<p class=MsoNormal align=center style='text-align:center'><span lang=EN-US-->
                                                                                <!--style='font-family:宋体;color:black'>0%</span></p>-->
              <!--</td>-->
            <!--</tr>-->
            <!--<tr style='height:18.45pt'>-->
              <!--<td width=131 style='width:98.0pt;border:dotted windowtext 1.0pt;border-top:-->
  <!--none;padding:0cm 18.0pt 0cm 18.0pt;height:18.45pt'>-->
                <!--<p class=MsoNormal align=center style='text-align:center'><span lang=EN-US-->
                                                                                <!--style='font-family:宋体;color:black'>ETH/</span><span lang=EN-US-->
                                                                                                                                    <!--style='font-family:宋体;color:black'>USDT</span></p>-->
              <!--</td>-->
              <!--<td width=200 style='width:149.9pt;border-top:none;border-left:none;-->
  <!--border-bottom:dotted windowtext 1.0pt;border-right:dotted windowtext 1.0pt;-->
  <!--padding:0cm 18.0pt 0cm 18.0pt;height:18.45pt'>-->
                <!--<p class=MsoNormal align=center style='text-align:center'><span lang=EN-US-->
                                                                                <!--style='font-family:宋体;color:black'>0%</span></p>-->
              <!--</td>-->
              <!--<td width=239 style='width:179.35pt;border-top:none;border-left:none;-->
  <!--border-bottom:dotted windowtext 1.0pt;border-right:dotted windowtext 1.0pt;-->
  <!--padding:0cm 18.0pt 0cm 18.0pt;height:18.45pt'>-->
                <!--<p class=MsoNormal align=center style='text-align:center'><span lang=EN-US-->
                                                                                <!--style='font-family:宋体;color:black'>0%</span></p>-->
              <!--</td>-->
            <!--</tr>-->
            <!--<tr style='height:18.45pt'>-->
              <!--<td width=131 style='width:98.0pt;border:dotted windowtext 1.0pt;border-top:-->
  <!--none;padding:0cm 18.0pt 0cm 18.0pt;height:18.45pt'>-->
                <!--<p class=MsoNormal align=center style='text-align:center'><span lang=EN-US-->
                                                                                <!--style='font-family:宋体;color:black'>GCX/</span><span lang=EN-US-->
                                                                                                                                    <!--style='font-family:宋体;color:black'>USDT</span></p>-->
              <!--</td>-->
              <!--<td width=200 style='width:149.9pt;border-top:none;border-left:none;-->
  <!--border-bottom:dotted windowtext 1.0pt;border-right:dotted windowtext 1.0pt;-->
  <!--padding:0cm 18.0pt 0cm 18.0pt;height:18.45pt'>-->
                <!--<p class=MsoNormal align=center style='text-align:center'><span lang=EN-US-->
                                                                                <!--style='font-family:宋体;color:black'>1%</span></p>-->
              <!--</td>-->
              <!--<td width=239 style='width:179.35pt;border-top:none;border-left:none;-->
  <!--border-bottom:dotted windowtext 1.0pt;border-right:dotted windowtext 1.0pt;-->
  <!--padding:0cm 18.0pt 0cm 18.0pt;height:18.45pt'>-->
                <!--<p class=MsoNormal align=center style='text-align:center'><span lang=EN-US-->
                                                                                <!--style='font-family:宋体;color:black'>1%</span></p>-->
              <!--</td>-->
            <!--</tr>-->
            <!--<tr style='height:18.45pt'>-->
              <!--<td width=131 style='width:98.0pt;border:dotted windowtext 1.0pt;border-top:-->
  <!--none;padding:0cm 18.0pt 0cm 18.0pt;height:18.45pt'>-->
                <!--<p class=MsoNormal align=center style='text-align:center'><span lang=EN-US-->
                                                                                <!--style='font-family:宋体;color:black'>LTC/</span><span lang=EN-US-->
                                                                                                                                    <!--style='font-family:宋体;color:black'>USDT</span></p>-->
              <!--</td>-->
              <!--<td width=200 style='width:149.9pt;border-top:none;border-left:none;-->
  <!--border-bottom:dotted windowtext 1.0pt;border-right:dotted windowtext 1.0pt;-->
  <!--padding:0cm 18.0pt 0cm 18.0pt;height:18.45pt'>-->
                <!--<p class=MsoNormal align=center style='text-align:center'><span lang=EN-US-->
                                                                                <!--style='font-family:宋体;color:black'>0%</span></p>-->
              <!--</td>-->
              <!--<td width=239 style='width:179.35pt;border-top:none;border-left:none;-->
  <!--border-bottom:dotted windowtext 1.0pt;border-right:dotted windowtext 1.0pt;-->
  <!--padding:0cm 18.0pt 0cm 18.0pt;height:18.45pt'>-->
                <!--<p class=MsoNormal align=center style='text-align:center'><span lang=EN-US-->
                                                                                <!--style='font-family:宋体;color:black'>0%</span></p>-->
              <!--</td>-->
            <!--</tr>-->
            <!--<tr style='height:18.45pt'>-->
              <!--<td width=131 style='width:98.0pt;border:dotted windowtext 1.0pt;border-top:-->
  <!--none;padding:0cm 18.0pt 0cm 18.0pt;height:18.45pt'>-->
                <!--<p class=MsoNormal align=center style='text-align:center'><span lang=EN-US-->
                                                                                <!--style='font-family:宋体;color:black'>DASH/</span><span lang=EN-US-->
                                                                                                                                     <!--style='font-family:宋体;color:black'>USDT</span></p>-->
              <!--</td>-->
              <!--<td width=200 style='width:149.9pt;border-top:none;border-left:none;-->
  <!--border-bottom:dotted windowtext 1.0pt;border-right:dotted windowtext 1.0pt;-->
  <!--padding:0cm 18.0pt 0cm 18.0pt;height:18.45pt'>-->
                <!--<p class=MsoNormal align=center style='text-align:center'><span lang=EN-US-->
                                                                                <!--style='font-family:宋体;color:black'>0%</span></p>-->
              <!--</td>-->
              <!--<td width=239 style='width:179.35pt;border-top:none;border-left:none;-->
  <!--border-bottom:dotted windowtext 1.0pt;border-right:dotted windowtext 1.0pt;-->
  <!--padding:0cm 18.0pt 0cm 18.0pt;height:18.45pt'>-->
                <!--<p class=MsoNormal align=center style='text-align:center'><span lang=EN-US-->
                                                                                <!--style='font-family:宋体;color:black'>0%</span></p>-->
              <!--</td>-->
            <!--</tr>-->
            <!--<tr style='height:18.45pt'>-->
              <!--<td width=131 style='width:98.0pt;border:dotted windowtext 1.0pt;border-top:-->
  <!--none;padding:0cm 18.0pt 0cm 18.0pt;height:18.45pt'>-->
                <!--<p class=MsoNormal align=center style='text-align:center'><span lang=EN-US-->
                                                                                <!--style='font-family:宋体;color:black'>ZEC/</span><span lang=EN-US-->
                                                                                                                                    <!--style='font-family:宋体;color:black'>USDT</span></p>-->
              <!--</td>-->
              <!--<td width=200 style='width:149.9pt;border-top:none;border-left:none;-->
  <!--border-bottom:dotted windowtext 1.0pt;border-right:dotted windowtext 1.0pt;-->
  <!--padding:0cm 18.0pt 0cm 18.0pt;height:18.45pt'>-->
                <!--<p class=MsoNormal align=center style='text-align:center'><span lang=EN-US-->
                                                                                <!--style='font-family:宋体;color:black'>0%</span></p>-->
              <!--</td>-->
              <!--<td width=239 style='width:179.35pt;border-top:none;border-left:none;-->
  <!--border-bottom:dotted windowtext 1.0pt;border-right:dotted windowtext 1.0pt;-->
  <!--padding:0cm 18.0pt 0cm 18.0pt;height:18.45pt'>-->
                <!--<p class=MsoNormal align=center style='text-align:center'><span lang=EN-US-->
                                                                                <!--style='font-family:宋体;color:black'>0%</span></p>-->
              <!--</td>-->
            <!--</tr>-->
            <!--<tr style='height:18.45pt'>-->
              <!--<td width=131 style='width:98.0pt;border:dotted windowtext 1.0pt;border-top:-->
  <!--none;padding:0cm 18.0pt 0cm 18.0pt;height:18.45pt'>-->
                <!--<p class=MsoNormal align=center style='text-align:center'><span-->
                  <!--style='font-family:宋体;color:black'>其他</span></p>-->
              <!--</td>-->
              <!--<td width=200 style='width:149.9pt;border-top:none;border-left:none;-->
  <!--border-bottom:dotted windowtext 1.0pt;border-right:dotted windowtext 1.0pt;-->
  <!--padding:0cm 18.0pt 0cm 18.0pt;height:18.45pt'>-->
                <!--<p class=MsoNormal align=center style='text-align:center'><span lang=EN-US-->
                                                                                <!--style='font-family:宋体;color:black'>0%</span></p>-->
              <!--</td>-->
              <!--<td width=239 style='width:179.35pt;border-top:none;border-left:none;-->
  <!--border-bottom:dotted windowtext 1.0pt;border-right:dotted windowtext 1.0pt;-->
  <!--padding:0cm 18.0pt 0cm 18.0pt;height:18.45pt'>-->
                <!--<p class=MsoNormal align=center style='text-align:center'><span lang=EN-US-->
                                                                                <!--style='font-family:宋体;color:black'>0%</span></p>-->
              <!--</td>-->
            <!--</tr>-->
          </table>

          <p class=MsoNormal align=left style='text-align:left;background:white'><span
            lang=EN-US style='font-family:宋体'>&nbsp;</span></p>

          <p class=MsoNormal align=left style='text-align:left;background:white'><span
            style='font-family:宋体'>提示</span></p>

          <p class=MsoNormal align=left style='text-align:left;background:white'><span
            lang=EN-US style='font-family:宋体'>1</span><span style='font-family:宋体'>、挂单是你所下的限价单并未与当前挂单成交，并被放在买卖盘中等待成交的摆单，它增加了买卖盘的流动性。</span></p>

          <p class=MsoNormal align=left style='text-align:left;background:white'><span
            lang=EN-US style='font-family:宋体'>2</span><span style='font-family:宋体'>、当其他人的摆单主动与你所下的摆单成交，你将支付挂单交易手续费（请注意当其他人的限价单与你的限价单成交，而下单时间又早于你时，你将支付吃单费）。</span></p>

          <p class=MsoNormal align=left style='text-align:left;background:white'><span
            lang=EN-US style='font-family:宋体'>3</span><span style='font-family:宋体'>、吃单是你所下的限价单或市价单与当前的挂单直接成交。</span></p>

          <p class=MsoNormal align=left style='text-align:left;background:white'><span
            lang=EN-US style='font-family:宋体'>4</span><span style='font-family:宋体'>、当你所下的摆单主动与其他人的摆单成交，你将支付吃单交易手续费。</span></p>

          <p class=MsoNormal align=left style='text-align:left;background:white'><span
            lang=EN-US style='font-family:宋体'>5</span><span style='font-family:宋体'>、交易手续费将从您的成交总额中扣除。若成交后获得比特币资产，则支付比特币交易手续费。</span></p>

          <p class=MsoNormal align=left style='text-align:left;background:white'><span
            lang=EN-US style='font-family:宋体'>&nbsp;</span></p>

          <p class=MsoNormal align=left style='text-align:left'><b><span
            style='font-family:宋体'>三、充币、提币</span></b><b><span
            style='font-family:宋体'>费率</span></b></p>

          <table class=MsoNormalTable border=1 cellspacing=0 cellpadding=0 align=left
                 width=0 style='background:white;border-collapse:collapse;border:none;'>
            <tr style='height:18.45pt'>
              <td width=131 style='width:98.0pt;border:dotted windowtext 1.0pt;padding:
  0cm 18.0pt 0cm 18.0pt;height:18.45pt'>
                <span lang=EN-US style='font-family:宋体;color:black'>&nbsp;</span>
              </td>
              <td width=200 style='width:149.9pt;border:dotted windowtext 1.0pt;border-left:
  none;padding:0cm 18.0pt 0cm 18.0pt;height:18.45pt'>
                <span style='font-family:宋体;color:black'>是否允许提币</span>
              </td>
              <td width=239 style='width:179.35pt;border:dotted windowtext 1.0pt;
  border-left:none;padding:0cm 18.0pt 0cm 18.0pt;height:18.45pt'>
                <span style='font-family:宋体;color:black'>提币手续费</span>
              </td>
              <td width=239 style='width:179.35pt;border:dotted windowtext 1.0pt;
  border-left:none;padding:0cm 18.0pt 0cm 18.0pt;height:18.45pt'>
                <span style='font-family:宋体;color:black'>最小提币额</span>
              </td>
              <td width=239 style='width:179.35pt;border:dotted windowtext 1.0pt;
  border-left:none;padding:0cm 18.0pt 0cm 18.0pt;height:18.45pt'>
                <span style='font-family:宋体;color:black'>是否允许充币</span>
              </td>
              <td width=239 style='width:179.35pt;border:dotted windowtext 1.0pt;
  border-left:none;padding:0cm 18.0pt 0cm 18.0pt;height:18.45pt'>
                <span style='font-family:宋体;color:black'>充币手续费</span>
              </td>
            </tr>
            <tr style="height: 18.45pt" v-for="(item,index) in fee">
              <td width=131 style='width:98.0pt;border:dotted windowtext 1.0pt;border-top:none;padding:0cm 18.0pt 0cm 18.0pt;height:18.45pt'>
                <span lang=EN-US style='font-family:宋体;color:black'>{{item.name}}</span>
              </td>
              <td width=200 style='width:149.9pt;border-top:none;border-left:none;
  border-bottom:dotted windowtext 1.0pt;border-right:dotted windowtext 1.0pt;
  padding:0cm 18.0pt 0cm 18.0pt;height:18.45pt'>
                <span lang=EN-US style='font-family:宋体;color:black'>{{item.enableWithdraw}}</span>
              </td>
              <td width=239 style='width:179.35pt;border-top:none;border-left:none;
  border-bottom:dotted windowtext 1.0pt;border-right:dotted windowtext 1.0pt;
  padding:0cm 18.0pt 0cm 18.0pt;height:18.45pt'>
                <span lang=EN-US style='font-family:宋体;color:black'>{{item.withdrawFee}}</span>
              </td>
              <td width=239 style='width:179.35pt;border-top:none;border-left:none;
  border-bottom:dotted windowtext 1.0pt;border-right:dotted windowtext 1.0pt;
  padding:0cm 18.0pt 0cm 18.0pt;height:18.45pt'>
                <span lang=EN-US style='font-family:宋体;color:black'>{{item.minWithdrawAmount}}</span>
              </td>
              <td width=239 style='width:179.35pt;border-top:none;border-left:none;
  border-bottom:dotted windowtext 1.0pt;border-right:dotted windowtext 1.0pt;
  padding:0cm 18.0pt 0cm 18.0pt;height:18.45pt'>
                <span lang=EN-US style='font-family:宋体;color:black'>{{item.enableRecharge}}</span>
              </td>
              <td width=239 style='width:179.35pt;border-top:none;border-left:none;
  border-bottom:dotted windowtext 1.0pt;border-right:dotted windowtext 1.0pt;
  padding:0cm 18.0pt 0cm 18.0pt;height:18.45pt'>
                <span lang=EN-US style='font-family:宋体;color:black'>{{item.rechargeFee}}</span>
              </td>
            </tr>
          </table>

          <p class=MsoNormal align=left style='text-align:left'><span lang=EN-US
                                                                      style='font-family:宋体'>&nbsp;</span></p>

          <p class=MsoNormal align=left style='text-align:left;background:white'><b><span
            style='font-family:宋体;background:white'>四、提</span></b><b><span
            style='font-family:宋体'>币</span></b><b><span style='font-family:宋体'>费率</span></b></p>

          <p class=MsoNormal align=left style='text-align:left;background:white'><span
            style='font-family:宋体'>提币平台不收取任何费用，但您需要支付矿工费。</span></p>

          <p class=MsoNormal align=left style='text-align:left;background:white'><span
            lang=EN-US style='font-family:宋体'>&nbsp;</span></p>

          <p class=MsoNormal align=left style='text-align:left;background:white'><span
            lang=EN-US style='font-family:宋体'>&nbsp;</span></p>

          <p class=MsoNormal align=left style='text-align:left;background:white'><span
            lang=EN-US style='font-family:宋体'>&nbsp;</span></p>

        </div>

      </div>
    </div>
  </div>
</template>
<style scoped>
  .agreement {
    background: #fff;
    padding-bottom: 20px;
    overflow-x:hidden;
  }

  .agreement_tab {
    height: 49px;
    text-align: center;
    margin-bottom: 20px;
    border-bottom: 1px solid #ccc;
  }

  .agreement_tab a {
    padding: 0 4px 16px;
    margin: 0 32px;
    color: #666;
    font-size: 14px;
    line-height: 48px;
  }

  .agreement_tab a.cur {
    color: #27abe2;
    font-weight: bold;
    border-bottom: 2px solid #27abe2;
  }

  /*.content {*/
    /*width: 1200px;*/
    /*margin: 0 auto;*/
    /*font-size:12px;*/
  /*}*/
  /*.content h3{*/
    /*font-size: 16px;*/
    /*padding-top: 10px;*/
  /*}*/
  .content table{
    margin: 10px 0;
    width: 100%;
    border: 1px solid #e6e6e6;
    border-spacing: 0;
    border-collapse: collapse;
  }
  .content table th,
  .content table td{
    border: 1px solid #e6e6e6 !important;
    font-weight: normal;
    padding: 0 24px;
    line-height: 36px;
    text-align: center;
  }

  .content{
    padding-top: 20px;
    /*padding-left: 200px;*/
    padding-bottom: 20px;
    text-align: left;
    padding-left: 20px;
    padding-right: 20px;
  }

  .content .ivu-col{
    text-align: left;
  }

  .content p{
    text-indent: 2em;
    margin-bottom: 10px;
    font-size: 14px;
  }
  .content>div{
    padding-bottom: 20px;
  }
  .content h3{
    font-size: 22px;
    font-weight: normal;
    margin-bottom: 20px;
  }
  .content h5 {
    font-size: 14px;
  }
  .WordSection1 span{ color:black;    font-family: 宋体;}
</style>
<script>
  export default {
    data(){
      return {
        symbol:[],
        fee:[]
      }
    },
    mounted:function () {
      this.getSymbol();
      this.getWithdrawFee();
    },
    methods:{
      getSymbol:function () {
        this.$http.post(this.host + '/market/symbol').then(response => {
          var result = response.body;
          this.symbol = result;
        });
      },
      getWithdrawFee:function () {
        this.$http.post(this.host + '/uc/coin/supported').then(response => {
            var result = response.body;
            this.fee = result;
            this.convertFee()
        })
      },
      convertFee:function () {
        for (var i = 0 ; i < this.fee.length ; i++) {
          switch (this.fee[i].name){
            case "Bitcoin":
              this.fee[i].name = "BTC";
              break;
            case "Bitcoincash":
              this.fee[i].name = "BCH";
              break;
            case "Ethereum":
              this.fee[i].name = "ETH";
              break;
            case "GalaxyChain":
              this.fee[i].name = "GCC";
              break;
            case "Litecoin":
              this.fee[i].name = "LTC";
              break;
          }

          switch (this.fee[i].enableWithdraw) {
            case "1":
              this.fee[i].enableWithdraw = "允许";
              break;
            default:
              this.fee[i].enableWithdraw = "不允许";
              break;
          }

          switch (this.fee[i].enableRecharge) {
            case "1":
              this.fee[i].enableRecharge = "允许";
              break;
            default:
              this.fee[i].enableRecharge = "不允许";
              break;
          }

          if (this.fee[i].withdrawFee.indexOf("E-") > -1) {
            var leftV = parseFloat(this.fee[i].withdrawFee.split("E-")[0]);
            var rightV = parseFloat(this.fee[i].withdrawFee.split("E-")[1]);
            for (var s=0;s<rightV;s++) {
              leftV = leftV / 10;
            }
            this.fee[i].withdrawFee = leftV;
          }

          this.fee[i].rechargeFee = 0;
        }
      },
      getFeeBySymbol:function (coin) {
        var fee = '0%';
        for (var i=0;i<this.symbol.length;i++){
            if(this.symbol[i].symbol == coin){
              fee = parseFloat(this.symbol[i].fee*100) + "%";
              break;
            }
        }
        return fee;
      }
    }
  }
</script>
