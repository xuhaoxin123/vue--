<template>
  <div>
    <div class="search">
      <input
        v-model="keyword"
        class="search-input"
        type="text"
        placeholder="输入城市名或拼音"
      />
    </div>
    <div class="search-content" ref="reference" v-show="keyword">
        <ul>
            <li class="search-item" v-for="item of List " ::key="item.id">
                  {{item.name}}
            </li>
            <li class="search-item border-bottom" v-show="hasNoData">
                没有找到匹配数据
              </li>
        </ul>
    </div>
  </div>
</template>

<script>
  import Bscroll from "better-scroll";

  export default {
    name: "CitySearch",
    props:{
      cities:Object
    },
    data() {
      return {
        keyword:'',
        List:[],
        timer: null
      };
    },
    computed: {
      hasNoData(){
          return !this.List.length
      }
    },
    watch: {
      keyword(){
        if(this.timer){
            clearTimeout(this.timer);
        }
        if(!this.keyword){
            this.List=[]
            return;
        }
        this.timer = setTimeout(()=>{
          const result = [];
            for(let i in this.cities) {
                // console.log(this.cities)
                this.cities[i].forEach((value)=>{
                    console.log(value)
                    if(value.spell.indexOf(this.keyword) >-1 || value.name.indexOf(this.keyword) > -1){
                            result.push(value)
                    }
                })
            }
            this.List = result;
        },100)
      }
    },
    mounted(){
      this.scroll = new Bscroll(this.$refs.reference)
    }
  };
</script>

<style lang="stylus" scoped>
  .search{
    height: .72rem;
    padding: 0 .1rem;
    background: #00bcd4;
    .search-input{
      box-sizing: border-box;
      width: 100%;
      height: .62rem;
      padding: 0 .1rem;
      line-height: .62rem;
      text-align: center;
      border-radius: .06rem;
      color: #666;
    }
  }
  .search-content{
    z-index: 1;
    overflow: hidden;
    position: absolute;
    top: 1.58rem;
    left: 0;
    right: 0;
    bottom: 0;
    background: #eee;
    .search-item{
      line-height: .62rem;
      padding-left: .2rem;
      background: #fff;
      color: #666;
    }
  }
</style>
