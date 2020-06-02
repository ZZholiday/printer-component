<template>
  <div class="print">
    <span>
      <button @click="print">打印</button>
      <input type="number" v-model="num" />份
    </span>

    <iframe id="iframe" style="display: none;"></iframe>
  </div>
</template>

<script>
export default {
  name: "PrintView",
  props: {
    html: {
      type: String,
      default: ""
    }
  },
  data() {
    return {
      num: 1
    };
  },
  methods: {
    print() {
      if (this.html) {
        this.setBodyHtml();
      }
    },
    setBodyHtml() {
      const iframe = window.frames[0];
      iframe.document.head.innerHTML = window.document.head.innerHTML;

      while (iframe.document.body.hasChildNodes()) {
        //当div下还存在子节点时 循环继续
        iframe.document.body.removeChild(iframe.document.body.firstChild);
      }
      let newHtml = `<div style="page-break-after:always;" >` + this.html + "</div>";
      let resultHtml = "";
      for (let i = 0; i < this.num; i++) {
        resultHtml += newHtml;
      }
      iframe.document.body.innerHTML = resultHtml;
      // eslint-disable-next-line no-unused-vars
      Promise.all([this.loadStyle(), this.loadImage()]).then(res => {
        //   打印
        iframe.window.print();
      });
    },
    loadStyle() {
      const iframe = window.frames[0];
      const styles = iframe.document.head.getElementsByTagName("style"); // <style>
      const links = iframe.document.head.getElementsByTagName("link"); // <link>
      let arrs = [];
      arrs = arrs.concat(...styles, ...links);
      // eslint-disable-next-line no-unused-vars
      return new Promise((resolve, reject) => {
        if (arrs.length) {
          for (let i = 0; i < arrs.length; i++) {
            arrs[i].onload = function() {
              if (i === arrs.length - 1) {
                resolve("style 样式加载完成");
              }
            };
          }
        } else {
          resolve("style 样式加载完成");
        }
      });
    },
    loadImage() {
      const iframe = window.frames[0];
      const imgs = iframe.document.body.getElementsByTagName("img"); // <img>
      // eslint-disable-next-line no-unused-vars
      return new Promise((resolve, reject) => {
        if (imgs.length) {
          for (let i = 0; i < imgs.length; i++) {
            imgs[i].onload = function() {
              if (i === imgs.length - 1) {
                resolve("img 加载完成");
              }
            };
          }
        } else {
          resolve("img 加载完成");
        }
      });
    }
  }
};
</script>

<style scoped>
</style>
