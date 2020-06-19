<template>
  <div>
    <div class="search-bar">
      <van-row class="test-row">
        <van-col span="3">
          <img :src="locationIcon" class="location-icon" />
        </van-col>
        <van-col span="16">
          <input type="text" class="search-input" />
        </van-col>
        <van-col span="5">
          <van-button size="mini">查找</van-button>
        </van-col>
      </van-row>
    </div>
    <div class="swiper-area">
      <van-swipe :autoplay="3000">
        <van-swipe-item v-for="(banner, index) in bannerPicArry" :key="index">
          <img v-lazy="banner.imageUrl" width="100%" />
        </van-swipe-item>
      </van-swipe>
    </div>
  </div>
</template>


<script>
import axios from "axios";
export default {
  data() {
    return {
      msg: "this is ShoppingMall",
      locationIcon: require("../../assets/images/location.png"),
      bannerPicArry: [
        {
          imageUrl:
            "https://images.baixingliangfan.cn/advertesPicture/20200612/20200612170403_599.jpg"
        },
        {
          imageUrl:
            "https://images.baixingliangfan.cn/advertesPicture/20200612/20200612170454_236.jpg"
        },
        {
          imageUrl:
            "https://images.baixingliangfan.cn/advertesPicture/20200612/20200612170514_5025.jpg"
        }
      ]
    };
  },
  created() {
    axios({
      url: "/api/api01.php",
      method: "get"
    })
      .then(response => {
        console.log(response);
      })
      .catch(error => {
        console.log(error);
      });
  }
};
</script>

<style scoped>
.search-bar {
  height: 2.2rem;
  vertical-align: middle;
  background-color: #e5017d;
  line-height: 2.2rem;
}
.location-icon {
  width: 40%;
}
.search-input {
  width: 100%;
  height: 1.3rem;
  border: 0px;
  border-bottom: 1px solid #fff;
  background-color: #e5017d;
  color: #fff;
}
.swiper-area {
  clear: both;
  max-height: 10rem;
  overflow: hidden;
}
</style>
