<!--
 * @Author: chenjm
 * @Date: 2022-09-21 11:18:50
 * @LastEditors: chenjm
 * @LastEditTime: 2022-09-21 14:33:36
 * @Description: 
-->
<template>
  <div class="canvas" id="canvas">
    <div class="canvas-btn">
      <div class="canvas-clear" id="canvasClear">
        <span>重写</span>
      </div>
      <div class="canvas-submit" id="canvasSubmit">
        <span>确认签名</span>
      </div>
    </div>
    <div class="canvas-box" id="canvasBox">
      <canvas id="canvasContent" class="canvas-content"> </canvas>
      <canvas class="canvas-rotate" id="canvasRotate"> </canvas>
    </div>
  </div>
</template>

<script>
export default {
  name: "h5Sign",
  methods: {
    renderingView() {
      var canvas = document.getElementById("canvasContent");
      var canvasBox = document.getElementById("canvasBox");
      var ctx = canvas.getContext("2d");
      canvas.height = canvasBox.clientHeight;
      canvas.width = canvasBox.clientWidth;
      canvas.addEventListener("touchstart", function (e) {
        e.preventDefault();
        ctx.beginPath();
        ctx.strokeStyle = "black";
        ctx.lineWidth = "4";
        var ev = e.touches[0] || window.event.touches[0];
        ctx.moveTo(
          ev.clientX - canvas.offsetLeft,
          ev.clientY - canvas.offsetTop
        );
        console.log(
          ev.clientX - canvas.offsetLeft,
          ev.clientY - canvas.offsetTop
        );
        canvas.addEventListener("touchmove", function (e1) {
          var ev1 = e1.touches[0] || window.event.touches[0];
          ctx.lineTo(
            ev1.clientX - canvas.offsetLeft,
            ev1.clientY - canvas.offsetTop
          );
          console.log(
            ev1.clientX - canvas.offsetLeft,
            ev1.clientY - canvas.offsetTop
          );
          ctx.stroke();
        });
      });
      document
        .getElementById("canvasClear")
        .addEventListener("click", function () {
          canvas.width = 0;
          canvas.height = 0;
          canvas.height = canvasBox.clientHeight;
          canvas.width = canvasBox.clientWidth;
        });
      document
        .getElementById("canvasSubmit")
        .addEventListener("click", function () {
          var canvas2 = document.getElementById("canvasRotate");
          var canvasBox = document.getElementById("canvasBox");
          var ctx2 = canvas2.getContext("2d");
          canvas2.width = canvasBox.clientWidth;
          canvas2.height = canvasBox.clientHeight;
          var img = new Image();
          img.src = canvas.toDataURL("image/png");
          img.onload = function () {
            ctx2.save(); //保存状态
            ctx2.translate(canvas2.width / 2, canvas2.height / 2); //设置画布上的(0,0)位置，也就是旋转的中心点
            ctx2.rotate((-90 * Math.PI) / 180); // 顺时针旋转90度
            ctx2.drawImage(img, -img.width / 2, -img.height / 2); //把图片绘制在旋转的中心点，
            ctx2.restore(); //恢复状态
            console.log(canvas2.toDataURL("image/png"));
          };
        });
    },
  },
  created() {
    this.$nextTick(() => {
      this.renderingView();
    });
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.canvas-box {
  flex: 4;
  overflow: hidden;
}

.canvas-btn {
  border-right: 1px solid #ccc;
  position: relative;
  flex: 1;
  background-color: #ffffff;
}
.canvas-btn div {
  position: absolute;
  width: 2.6rem;
  height: 2.6rem;
  left: 50%;
  transform: translate(-50%, 0);
  /* writing-mode: tb-rl; */
  text-align: center;
  border: 2px solid #1a9bff;
  border-radius: 8px;
}
.canvas-clear {
  top: 5%;
  color: #1a9bff;
}
.canvas-clear span {
  margin: 0.05rem;
}
.canvas-submit {
  bottom: 5%;
  background-color: #1a9bff;
  color: #fff;
}
.canvas {
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  background-color: #fff;
  z-index: 9999;
  display: flex;
}
.canvas-btn span {
  display: inline-block;
  transform: rotate(90deg);
  /* margin: 0.05rem; */
}
.canvas-rotate {
  visibility: hidden;
}
</style>
