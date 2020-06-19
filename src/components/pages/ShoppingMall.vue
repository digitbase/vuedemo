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
  </div>
</template>

<script>
export default {
  data() {
    return {
      msg: "this is ShoppingMall",
      locationIcon: require("../../assets/images/location.png")
    };
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
</style>
