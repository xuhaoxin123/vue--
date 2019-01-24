<template>
  <div>
    <home-header :city="city"></home-header>
    <home-swiper :list="swiperList"></home-swiper>
    <home-icons  :list="iconList"></home-icons>
    <home-recommend :list="recommendList"></home-recommend>
    <home-weekend :list="weekendList"></home-weekend>
  </div>
</template>

<script>
  import HomeHeader from "./components/Header";
  import HomeSwiper from "./components/Swiper";
  import HomeIcons from "./components/Icons";
  import HomeRecommend from "./components/Recommend";
  import HomeWeekend from "./components/Weekend";
  import axios from "axios";
  export default {
    data() {
      return {
       city:'',
       swiperList:[],
       iconList:[],
       recommendList: [],
      weekendList: []
      };
    },
    name: "home",
    components: {
      HomeHeader,
      HomeSwiper,
      HomeIcons,
      HomeWeekend,
      HomeRecommend
    },
    methods: {
      getHomeInfo() {
        axios.get("/api/index.json").then(res => {
          console.log(res);
          if(res.data){
            console.log('0000000000000000000000000')
            const data= res.data.data;
            console.log(data)
            this.swiperList = data.swiperList
            this.iconList = data.iconList
            this.recommendList = data.recommendList
            this.weekendList = data.weekendList
          }
        });
      }
    },
    mounted() {
      this.getHomeInfo()
    }
  };
</script>
