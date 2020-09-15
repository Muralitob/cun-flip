<!--
 * @Author: Mura
 * @Date: 2020-09-12 22:15:53
 * @LastEditors: Mura
 * @LastEditTime: 2020-09-15 14:18:31
 * @Description: 描述一下咯
 * @@Copyrigh: © 2020 杭州杰竞科技有限公司 版权所有
-->
<template>
  <div class="menu">
    <div class="menu-btn" @click="toggle"></div>
    <transition
      v-bind:css="false"
      v-on:before-enter="beforeEnter"
      v-on:enter="enter"
      v-on:after-enter="afterEnter"
      v-on:before-leave="beforeleave"
      v-on:leave="leave"
      v-on:after-leave="afterleave"
    >
      <div class="menu-content" v-show="show">
        <!-- <ListAnimation>
          <div v-for="(item, index) in lists" data-x="-200px" data-y="-500px"  data-s="2" class="content" :key="item.key" :data-delay="index*50" ></div>
        </ListAnimation>
         -->
          <div class="content lg" key="1"></div>
          <div class="content" key="2"></div>
          <div class="content sm" key="3"></div>
          <div class="content" key="4"></div>
          <div class="content sm" key="5"></div>
      </div>
    </transition>
  </div>
</template>

<script>
import ListAnimation from 'vue-list-animation';
console.log('ListAnimation', ListAnimation);
export default {
  components: { ListAnimation },
  data() {
    return {
      show: false,
      SPEED: 200,
      firstReact: {},
      transitionType: "",
      include: [],
      lists: [],
    };
  },
  mounted() {
    setTimeout(() => {
      this.lists = [
        {
          key: 1,
          c: 'lg'
        },
        {
          key: 2,
        },
        {
          key: 3,
          c: 'sm'
        },
        {
          key: 4,
        },
        {
          key: 5,
          c: 'sm'
        },
      ]  
    }, 1000)
  },
  methods: {
    toggle() {
      this.show = !this.show;
    },
    beforeEnter(dom) {
      this.firstReact = dom.getBoundingClientRect();
      dom.style.cssText = `transition: all ${this.SPEED}ms;top:0px;left: 0px`;
    },
    enter(dom, done) {
      console.log("in");
      var lastReact = dom.getBoundingClientRect();
      console.log(lastReact);
      var Invert = {
        deltax: this.firstReact.left - lastReact.left,
        deltaY: this.firstReact.top - lastReact.top,
        deltaW: this.firstReact.width / lastReact.width,
      };
      console.log(Invert);
      //paly
      dom.animate(
        [
          {
            width: "150px",
            height: "40px",
            left: "0px",
            top: "0px",
          },
          {
            width: `${lastReact.width}px`,
            height: `${lastReact.height}px`,
            left: `-200px`,
            top: `-420px`,
          },
        ],
        {
          duration: this.SPEED,
        }
      ).onfinish = function () {
        console.log("onfinish");
        done(); //调用done() 告诉vue动画已完成，以触发 afterEnter 钩子
      };
    },
    afterEnter(dom) {
      dom.style.cssText = "";
    },
    beforeleave(dom) {
      console.log("out");
      dom.style.cssText = `transition: all ${this.SPEED}ms;top:0px;left: 0px`;
      if (this.SLIDE) {
        dom.style.cssText = `transition: transform ${this.SPEED}ms;transform: translate(0, 0);`;
      }
    },
    leave(dom, done) {
      console.log("out");
      var lastReact = dom.getBoundingClientRect();
      console.log(lastReact);
      var Invert = {
        deltax: this.firstReact.left - lastReact.left,
        deltaY: this.firstReact.top - lastReact.top,
        deltaW: this.firstReact.width / lastReact.width,
      };
      console.log(Invert);
      //paly
      dom.animate(
        [
          {
            width: "150px",
            height: "40px",
            left: "0px",
            top: "0px",
          },
          {
            width: `${lastReact.width}px`,
            height: `${lastReact.height}px`,
            left: `-200px`,
            top: `-420px`,
          },
        ],
        {
          duration: this.SPEED,
          direction: "reverse",
        }
      ).onfinish = function () {
        console.log("onfinish");
        done(); //调用done() 告诉vue动画已完成，以触发 afterEnter 钩子
      };
    },
    afterleave(dom) {
      // dom.style.cssText = "";
    },
  },
};
</script>

<style>
.menu {
  position: relative;
  position: absolute;
  right: 5vw;
  bottom: 20vw;
}
.menu-btn {
  width: 150px;
  height: 40px;
  background-color: #4676ab;
  border-radius: 10px;
  box-shadow: 0 10px 20px -4px #4676ab;
  z-index: 999;
  transition: 0.3s all cubic-bezier(0, 1, 0.95, 1.05);
}
.menu-btn:hover {
  transform: scale(0.95);
}
.menu-content {
  width: 350px;
  height: 400px;
  background-color: #4676ab;
  border-radius: 10px;
  box-shadow: 0 10px 20px -4px #4676ab;
  z-index: 999;
  position: absolute;
  top: -420px;
  left: -200px;
  vertical-align: bottom;
  overflow: hidden;
}
.content {
  background-color: #fefefc;
  width: 70%;
  height: 24px;
  border-radius: 10px;
  display: flex;
  flex-direction: column;
  margin: 24px;
}
.lg {
  background-color: #fff;
  width: 80%;
  height: 48px;
}
.sm {
  width: 50%;
}
</style>