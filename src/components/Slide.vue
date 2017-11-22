<template>
  <div class="slide" :style="{'width':`${imgWidth}px`, 'height':`${imgHeight}px`}">
    <ul :style="{'width':`${imgWidth*imgList.length}px`,'transform':`translateX(-${imgWidth*nowIndex}px`}">
      <li v-for="(img, index) of imgList" :key="img.id" :style="{'width':`${imgWidth}`}">
        <img :src="img" alt="img" :style="{'width':`${imgWidth}px`, 'height':`${imgHeight}px`}">
      </li>
    </ul>
    <div class="arrow">
      <span class="arrow-left" @click.stop="btnArrow('left')"></span>
      <span class="arrow-right" @click.stop="btnArrow"></span>
    </div>
    <div class="option">
      <span v-for="(img, index) of imgList" :key="index" :class="{'active':index===nowIndex}" @click.stop="btnOption(index)">
      </span>
    </div>
  </div>
</template>
<script>
  export default {
    name: 'slide',
    data() {
      return {
        nowIndex: 0,
        imgWidth: 720,
        imgHeight: 480,
        timer: 0,
        imgList: [
          'static/images/img1.jpg',
          'static/images/img2.jpg',
          'static/images/img3.jpg',
          'static/images/img4.jpg'
        ]
      };
    },
    methods: {
      // 左右切换按钮
      btnArrow(left) {
        clearInterval(this.timer);
        if (left === 'left') {
          this.nowIndex === 0 ? this.nowIndex = this.imgList.length - 1 : this.nowIndex--;
        } else this.nowIndex === this.imgList.length - 1 ? this.nowIndex = 0 : this.nowIndex++;
        this.timer = setInterval(() => {
          this.btnArrow();
        }, 3000);
      },
      // 下方圆点切换按钮
      btnOption(index) {
        clearInterval(this.timer);
        this.nowIndex = index;
        this.timer = setInterval(() => {
          this.btnArrow();
        }, 5000);
      }
    },

    mounted() {
      this.timer = setInterval(() => {
        this.btnArrow();
      }, 3000);
    }
  };

</script>
style
<style lang="scss">
  .slide {
    font-size: 16px;
    overflow: hidden;
    position: relative;
    margin: 2em auto;
    border-radius: 4px;

    background-color: #fff;

    box-shadow: 0 6px 8px rgba(102, 119, 136, 0.03),
    0 1px 2px rgba(102, 119, 136, 0.3), 0 1px 6px rgba(32, 33, 36, 0.28);

    transition: all 0.5s ease-in-out;
    ul {
      display: flex;

      list-style: none;

      margin: 0;
      padding: 0;

      flex-direction: row;
    }
    // 左右三角按钮
    %arrow {
      position: absolute;
      top: 0;
      bottom: 0;

      width: 0;
      height: 0;
      margin: auto;
      border-top: 10px solid transparent;
      border-bottom: 10px solid transparent;
    }
    .arrow-right {
      @extend %arrow;

      right: 2em;

      border-left: 20px solid rgba(255, 255, 255, 0.5);
      &:hover {
        border-left: 20px solid rgba(255, 255, 255, 1);
      }
    }
    .arrow-left {
      @extend %arrow;

      left: 2em;

      border-right: 20px solid rgba(255, 255, 255, 0.5);
      &:hover {
        border-right: 20px solid rgba(255, 255, 255, 1);
      }
    }
    // 下方圆点选项
    .option {
      position: absolute;
      bottom: 2em;
      left: 0;

      width: 100%;
      margin: auto;

      text-align: center;
      span {
        display: inline-block;

        width: 1em;
        height: 1em;
        margin: 0 0.5em;
        border-radius: 50%;

        background-color: rgba(255, 255, 255, 0.5);
        &.active {
          background-color: rgba(255, 255, 255, 1);
        }
      }
    }
  }

</style>
