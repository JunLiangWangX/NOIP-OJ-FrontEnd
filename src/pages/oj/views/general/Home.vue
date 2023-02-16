<!--
 * @Description: 首页
 * @Author: JunLiangWang
 * @Date: 2023-02-13 18:11:48
 * @LastEditors: JunLiangWang
 * @LastEditTime: 2023-02-15 16:49:17
-->
<template>
  <div class='home-page'>
    <Carousel class="carousel-container" v-model="value1">
      <Carousel-item>
        <div class="carousel-content slogan">
          <video src="@/assets/home3.webm" ref="videoPlayer" loop autoplay muted />
          <div class="slogan-container">
            <span>算法之美</span>
            <span>不止于此</span>
          </div>
        </div>
      </Carousel-item>
      <Carousel-item>
        <div class="carousel-content">2</div>
      </Carousel-item>
      <Carousel-item>
        <div class="carousel-content">3</div>
      </Carousel-item>
      <Carousel-item>
        <div class="carousel-content">4</div>
      </Carousel-item>
    </Carousel>
  </div>
</template>

<script>
export default {
  name: 'home'
}
</script>

<style lang="less" scoped>
.home-page {
  width: 100%;
  height: 100%;
}

.carousel-container,
.carousel-content,
.carousel-content video {
  width: 100%;
  height: 100%;
}

.carousel-content video {
  object-position: center;
  object-fit: cover;
}
.slogan{
  position: relative;
}
.slogan-container{
  position: absolute;
    top: 0;
    right: 0;
    left: 0;
    bottom: 0;
    margin: auto;
    height: 110px;
    text-align: center;
    font-size: 74px;
	-webkit-animation: tracking-in-expand-fwd-bottom 1s cubic-bezier(0.215, 0.610, 0.355, 1.000) both;
	        animation: tracking-in-expand-fwd-bottom 1s cubic-bezier(0.215, 0.610, 0.355, 1.000) both;
    span{
      margin: 0 30px;
    }
}
 @-webkit-keyframes tracking-in-expand-fwd-bottom {
  0% {
    letter-spacing: -0.5em;
    -webkit-transform: translateZ(-700px) translateY(500px);
            transform: translateZ(-700px) translateY(500px);
    opacity: 0;
  }
  40% {
    opacity: 0.6;
  }
  100% {
    -webkit-transform: translateZ(0) translateY(0);
            transform: translateZ(0) translateY(0);
    opacity: 1;
  }
}
@keyframes tracking-in-expand-fwd-bottom {
  0% {
    letter-spacing: -0.5em;
    -webkit-transform: translateZ(-700px) translateY(500px);
            transform: translateZ(-700px) translateY(500px);
    opacity: 0;
  }
  40% {
    opacity: 0.6;
  }
  100% {
    -webkit-transform: translateZ(0) translateY(0);
            transform: translateZ(0) translateY(0);
    opacity: 1;
  }
}

</style>
<style>
.home-page .ivu-carousel-list,
.home-page .ivu-carousel-track,
.home-page .ivu-carousel-item {
  width: 100%;
  height: 100% !important;
}
</style>