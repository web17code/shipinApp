<template>
  <div id="app">
    <meta name="viewport"
          content="height=device-height,width=device-width,initial-scale=1,maximum-scale=1,minimum-scale=1,user-scalable=no"/>
    <router-view/>
    <!--底部导航-->
    <!--<mu-paper style="position: fixed;bottom:0;width: 100%;">
      <mu-bottom-nav :value="bottomNav"
                     @change="handleChange"
                     v-show="!($route.path.indexOf('_nobar') > 0)">
        <mu-bottom-nav-item value="home" title="首页" icon="favorite"/>
        <mu-bottom-nav-item value="user" title="我的" icon="account_circle"/>
      </mu-bottom-nav>
    </mu-paper>-->
    <div class="NavigiteBottomBar" v-show="!($route.path.indexOf('_nobar') > 0)">
      <div @click="handleChange('home')" :class="[nowBar=='home'?'active':'','NBBarItem']">
        <img src="./assets/ic_favorite_black_24px.svg"
             v-show="nowBar!='home'"
             alt="">
        <img src="./assets/ic_favorite_blue_24px.svg"
             v-show="nowBar=='home'"
             alt=""><p>首页</p>
      </div>
      <div @click="handleChange('user')" :class="[nowBar=='user'?'active':'','NBBarItem']">
        <img src="./assets/ic_account_circle_black_24px.svg"
             v-show="nowBar!='user'"
             alt="">
        <img src="./assets/ic_account_circle_blue_24px.svg"
             v-show="nowBar=='user'"
             alt=""><p>我的</p>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'app',
    data: function () {
      return {
        nowBar:'home',
        isShowBar: true,//是否显示tab栏
        bottomNav: ""
      }
    },
    methods: {
      handleChange: function (val) {//切换底部的tab
        //console.log(val);
        this.bottomNav = val;
        this.nowBar = val;
        this.$router.replace({path: val})//, query: {user: "zhuhj"}
        if (this.$route.path.indexOf("_nobar") > 0) {//有"_nobar"隐藏tab切换
          this.isShowBar = false;
        } else {
          this.isShowBar = true;
        }
      }
    }
  }
</script>

<style>
  * {
    margin: 0;
    padding: 0;
  }

  input, select, option, textarea {
    outline: none;
  }

  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    font-size: 62.5%;
  }

  .cf17 {
    clear: both;
    content: "";
    display: block;
  }

  .submitBtn {
    font-size: 1rem;
  }

  .NavigiteBottomBar {
    background-color: #fff;
    height: 56px;
    display: flex;
    flex-direction: row;
    position: fixed;
    bottom: 0;
    width: 100%;
    border-top:1px solid #ddd;
  }
  .NBBarItem{
    font-size: 0.8rem;
    padding: 6px;
    width: 50%;
    height: 100%;
    display: flex;
    flex-direction: column;
  }
  .NBBarItem.active{
    color:#03a9f4;
  }
  /*change searchInput css*/
  /*.appbar-search-field {
    color: #FFF;
    margin-bottom: 0;
  }
  .appbar-search-field.focus-state {
    color: #FFF;
  }
  .appbar-search-field .mu-text-field-hint {
    color: rgba(255, 255, 255, 0.54);
  }
  .appbar-search-field .mu-text-field-input {
    color: #FFF;
  }
  .appbar-search-field .mu-text-field-focus-line {
    background-color: #FFF;
  }
  .hintTextClass{
    text-align: left;
  }*/
</style>
