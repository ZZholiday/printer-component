<template>
  <div class="pharmacy">
    <div class="title">深圳问止中医投资发展有限公司问止中医诊所</div>
    <div class="form">
      <div style="display: flex;flex-flow:  row nowrap;justify-content: space-between;">
        <div>姓名：李大泽</div>
        <div>性别：男</div>
        <div>年龄：29</div>
        <div>电话：*********1729</div>
      </div>
      <div style="display: flex;">
        <div style="margin-right:70px;line-height: 2.5;">日期：2020/5/21</div>
        <div style="margin-right:70px;line-height: 2.5;">剂数：5剂</div>
        <div style="margin-right:70px;line-height: 2.5;">用量：200ml</div>
      </div>
      <div style="display: flex;">
        <div>服药时间：每日两次，早晚饭后一小时温服</div>
      </div>
    </div>
    <div class="flex">
      <div class="left-part">
        <hr />医嘱：忌饮酒，忌寒凉食物(水果、冰品等)，忌熬夜，忌过劳，忌久坐，忌咖啡，忌牛奶，忌房事，忌睡前喝茶，忌食动物内脏，忌抽烟，忌吃油炸食物，忌大怒，忌辛辣，宜多走路，宜保暖
      </div>
      <div class="right-part">
        <div class="qrcode" id="qrcode"></div>
      </div>
    </div>
  </div>
</template>

<script>
import QRCode from "qrcodejs2";
export default {
  name: "Pharmacy",
  props: {
    msg: String
  },
  created() {
    this.$nextTick(function() {
      // eslint-disable-next-line no-unused-vars
      var qrcode = new QRCode("qrcode", {
        width: 170,
        height: 170,
        text: "www.baidu.com", //表示内容，可以是地址或者是文字'55566'或者参数
        colorDark: "#000000", //前景色
        colorLight: "#ffffff", //背景色
        correctLevel: QRCode.CorrectLevel.H //容错级别
      });
    });
  },
  mounted() {}
};
</script>


<style scoped>
.pharmacy {
  line-height: 1.5;
  font-size: 1.3rem;
  width: 700px;
  height: 400px;
  padding: 20px;
}
.form {
}
.flex {
  display: flex;
}
hr {
  margin-block-start: 0.7em;
  margin-block-end: 0.7em;
  border-width: 2px;
  border-style: solid;
  color: #CCC;
}
.left-part {
  margin-right: 25px;
  margin-bottom: 25px;
}
.right-part {
  
}
.title {
  text-align: center;
  font-size: 2rem;
  margin: 10px 30px;
}
</style>