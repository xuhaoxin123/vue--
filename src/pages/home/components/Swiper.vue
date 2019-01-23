<template>
  <swiper :options="swiperOption" ref="mySwiper" class="swiper">
    <!-- slides -->
    <swiper-slide v-for="item of swiperList" :key="item.id"> <img :src="item.imgUrl" class="swiper-img" /> </swiper-slide>
  </swiper>
</template>

<script>
  export default {
    name: "carrousel",
    data() {
      return {
        swiperOption: {
          // some swiper options/callbacks
          // 所有的参数同 swiper 官方 api 参数
          // ...
        },
        swiperList:[
          {id:1,imgUrl:'https://imgs.qunarzz.com/vc/42/26/bb/71d41bf5d04fcb589ece936cba.jpg_92.jpg'},
          {id:2,imgUrl:'https://imgs.qunarzz.com/vc/42/26/bb/71d41bf5d04fcb589ece936cba.jpg_92.jpg'}
      ]
      };
    },
    computed: {
      swiper() {
        return this.$refs.mySwiper.swiper;
      }
    },
    mounted() {
      // current swiper instance
      // 然后你就可以使用当前上下文内的swiper对象去做你想做的事了
      console.log("this is current swiper instance object", this.swiper);
      this.swiper.slideTo(3, 1000, false);
    }
  };
</script>

<style lang="scss" scoped>
  .swiper {
    overflow: hidden;
    width: 100%;
    height: 0;
    padding-bottom: 31.5%;
  }
  .swiper-img {
    width: 100%;
  }
</style>
