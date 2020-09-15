<!--
 * @Author: Mura
 * @Date: 2020-09-01 14:20:51
 * @LastEditors: Mura
 * @LastEditTime: 2020-09-14 22:41:35
 * @Description: 描述一下咯
 * @@Copyrigh: © 2020 杭州杰竞科技有限公司 版权所有
-->
<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <router-view/>
    <div>
      <ExpandMenu />
    </div>
  </div>
</template>
<script>
import ExpandMenu from './views/ExpandMenu';
export default {
  components: { ExpandMenu }
}
</script>
<style>
body, html {
  margin: 0;
  padding: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  overflow: hidden;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
