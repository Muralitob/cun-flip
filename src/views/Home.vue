<!--
 * @Author: Mura
 * @Date: 2020-09-01 14:20:51
 * @LastEditors: Mura
 * @LastEditTime: 2020-09-14 21:53:11
 * @Description: 描述一下咯
 * @@Copyrigh: © 2020 杭州杰竞科技有限公司 版权所有
-->
<template>
  <div class="home">
    <div class="m-list" :style="{transform: 'translate(' + current * -84 + 'vw)' }">
      <div class="m-item" v-for="(item, index) in 6" :key="index" @touchstart="touchstart" @touchend="touchend" >
        {{ index }}
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'Home',
  data() {
    return {
      list: [
        {
          title: '111'
        }
      ],
      current: 2,
      startX: 0,
    }
  },
  methods: {
    touchstart(e) {
      this.startX = e.touches[0].clientX
    },
    touchend(e) {
      const WIDTH = window.innerWidth / 2
      let endX = e.changedTouches[0].clientX
      if( (endX - this.startX ) > WIDTH ) {
        this.current > 0 && this.current--
      }else if (this.startX - endX > WIDTH) {
        this.current < 5 && this.current++
      }
    }
  }
}
</script>

<style>
  .home {
    width: 600%;
    height: 100vh;
    overflow: hidden;
  }
  .m-list {
    display: flex;
    height: 100%;
    width: 100%;
    transition: .3s all cubic-bezier(0, 1, 0.95, 1.05);
  }
  .m-item {
    background-color: rgb(130,185,246);
    border-radius: 10px;
    height: 80%;
    width: 80vw;
    margin: 0 2vw;
    box-shadow: 0 10px 20px -4px rgba(106, 182, 252, .5);
    color: #000;
    text-align: center;
    line-height: 200px;
    font-size: 42px;
  }
  .m-item:first-child {
    margin-left: 10vw;
  }
</style>