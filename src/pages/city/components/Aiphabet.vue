<template>
  <ul class="list">
    <li
      class="item"
      v-for="item of letters"
      :key="item"
      @click="handleLetterClick"
      @touchstart="handleTouchStart"
      @touchmove="handleTouchMove"
      @touchend="handleTouchEnd"
      :ref="item"
    >
      {{ item }}
    </li>
  </ul>
</template>

<script>
  export default {
    name: "CityAlphabet",
    props: {
      cities: Object
    },
    data() {
      return {
        touchStatus: false,
        startY: 0,
        timer:null
      };
    },
    computed: {
      letters() {
        const letters = [];
        for (let i in this.cities) {
          letters.push(i);
        }
        console.log(letters);
        return letters;
      }
    },
    updated() {
      this.startY = this.$refs["A"][0].offsetTop;
    },
    methods: {
      handleLetterClick(e) {
        this.$emit("change", e.target.innerText);
        console.log(e.target.innerText);
      },
      handleTouchStart() {
        this.touchStatus = true;
      },
      handleTouchMove(e) {
        if (this.touchStatus) {
          if (this.timer) {
            clearTimeout(this.timer);
          }
          this.timer = setTimeout(() => {
            const touchY = e.touches[0].clientY - 79;
            const index = Math.floor((touchY - this.startY) / 20);
            if (index >= 0 && this.letters.length) {
              this.$emit("change", this.letters[index]);
            }
          }, 16);
        }
      },
      handleTouchEnd() {
        this.touchStatus = false;
      }
    }
  };
</script>
<style lang="scss" scoped>
  .list {
    display: flex;
    flex-direction: column;
    justify-content: center;
    position: absolute;
    top: 1.58rem;
    right: 0;
    bottom: 0;
    width: 0.4rem;
    .item {
      line-height: 0.4rem;
      text-align: center;
      color: #00bcd4;
    }
  }
</style>
