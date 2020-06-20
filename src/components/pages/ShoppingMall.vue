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
    <div class="type-bar">
      <div v-for="(cate, index) in category" :key="index">
        <img v-lazy="cate.image" />
        <span>{{ cate.mallCategoryName }}</span>
      </div>
    </div>

    <div class="recommend-area">
      <div class="recommend-title">
        商品推荐
      </div>
      <div class="recommend-body">
        <div v-for="(item, index) in recommendGoods" :key="index">
          <!-- <swiper-slide class="recommend-item">
            <img :src="item.image" width="80%" />
            <div>{{ item.goodsName }}</div>
            <div></div>
          </swiper-slide> -->
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import { Swiper, SwiperSlide, directive } from "vue-awesome-swiper";
import "swiper/css/swiper.css";

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
      ],
      category: [],
      recommendGoods: []
    };
  },
  components: { Swiper, SwiperSlide },
  directives: {
    swiper: directive
  },
  swiperOption: {
    spaceBetween: 30,
    effect: "fade",
    pagination: {
      el: ".swiper-pagination",
      clickable: true
    },
    navigation: {
      nextEl: ".swiper-button-next",
      prevEl: ".swiper-button-prev"
    }
  },
  created() {
    axios({
      url: "/api/api01.php",
      method: "get"
      //responseType: "json"
    })
      .then(response => {
        if (response.status == 200) {
          let data = eval("(" + response.data + ")");
          this.category = data.data.category;
          this.recommendGoods = data.data.recommend;
          console.log(this.recommendGoods);
        }
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
.type-bar {
  background: #e5017d;
  float: left;
  border-radius: 0.3rem;
  font-size: 12px;
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
}
.type-bar div {
  width: 3rem;
  padding: 0.3rem;
}
.type-bar img {
  width: 99%;
}
.recommend-area {
  background-color: #fff;
  margin-top: 3rem;
}
.recommend-title {
  border-bottom: 1px solid #eee;
  font-size: 14px;
}
</style>
