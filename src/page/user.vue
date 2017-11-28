<style scoped>
  /**
  * Created by web17code
  */
  .userContent{
    min-height: 100vh;
    background-color: #e8e8e8;
  }
  .InfoContent{
    padding:0 0.3rem;
    border-bottom:1px solid #999;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content:flex-start;
    height:5rem;
    background-color: #fff;
  }
  .InfoContent img.avatar{
    display: flex;
    width:3.5rem;
    height: 3.5rem;
    border-radius: 50%;
    border:1px solid #ddd;
  }
  .InfoContent .infoTxt{
    display: flex;
    flex-direction: column;
    padding: 1rem 0;
    align-self:flex-start;
    margin-left: 1.5rem;
    flex: 1;
  }
  .InfoContent .infoTxt .infoTxtName{
    font-size:0.9rem;
    line-height: 1.5rem;
    display: flex;
  }
  .InfoContent .infoTxt .infoTxtType{
    font-size:0.9rem;
    display: flex;
    line-height: 1.5rem;
  }
  .startContent{
    padding:0 0.3rem;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    height:5rem;
    background-color: #fff;
    border-bottom:1px solid #E8E8E8;
  }
  .startContent div.txt{
    font-size: 1.1rem;
    display: flex;
    flex-direction: column;
    padding: 1rem 0;
    margin-left: 1.5rem;
  }
  .rightArr{
    display: flex;
    width: 1.5rem;
    height: 1.5rem;
    margin-right: 0rem;
  }
</style>

<template>
  <div class="userContent">
    <!--标题bar-->
    <appHeaderBar text="我的" :isHideLeft="true" :isHideRight="false"></appHeaderBar>
    <div class="InfoContent" @click="goLogin">
      <img class="avatar" v-show="avatarUrl"
            alt="头像" :src="avatarUrl?avatarUrl:''">
      <img src='../assets/personAVATAR.png' alt="头像"
           class="avatar"
           v-show="!avatarUrl">
      <div class="infoTxt">
        <p class="infoTxtName">用户名：{{Username}}</p>
        <p class="infoTxtType">普通会员</p>
      </div>
      <img src="../assets/rightArr.svg"
           @click="goLogin"
           class="rightArr">
    </div>
    <!--收藏页-->
    <div class="startContent" @click="goStarList" style="margin-top: 2rem;">
      <div class="txt">
        <span>收藏列表</span>
      </div>
      <img src="../assets/rightArr.svg"
           @click="goStarList"
           class="rightArr">
    </div>
    <div class="startContent" @click="goAbout">
      <div class="txt">
        <span>关于</span>
      </div>
      <img src="../assets/rightArr.svg"
           @click="goAbout"
           class="rightArr">
    </div>
    <!--退出提示模态框-->
    <div>
      <mu-dialog :open="dialog" title="通知" @close="close">
        {{MsgText}}
        <mu-flat-button slot="actions" primary @click="close" label="取消"/>
        <mu-flat-button slot="actions" primary @click="loginOut" label="确定"/>
      </mu-dialog>
    </div>
  </div>
</template>

<script>
  import appHeader from "../components/appHeader.vue"
  export default {
    data: function () {
      return {
        MsgText:"",
        Username:"",
        dialog:false,
        avatarUrl:false
      }
    },
    props: {},
    methods: {
      close:function(){
        this.dialog = false;
      },
      goLogin:function(){
        //查看是否登录
        var that = this;
        //检查登陆
        this.$http.post(window.getHost + 'wap/main/getloginUser', {}, {emulateJSON: true})
          .then(function (data) {
            console.log(data.data);
            if (!data.data.success) {
              this.$router.push({
                path: "login_nobar",query:{}
              })
            }else{
              that.dialog = true;
              that.MsgText = "您要注销登录吗";
            }
          })
      },
      goStarList:function(){
        this.$router.push({
          path: "starList_nobar",query:{}
        })
      },
      goAbout:function(){
        this.$router.push({
          path: "about_nobar",query:{}
        })
      },
      loginOut:function(){
        var that = this;
        this.$http.post(window.getHost + 'wap/uc/exit', {}, {emulateJSON: true})
          .then(function (data) {
            this.dialog = false;
            if (data.data.success) {
              that.Username = "已注销";
            }
          })
      }
    },
    created: function () {
      var that = this;
      //检查登陆
      this.$http.post(window.getHost + 'wap/main/getloginUser', {}, {emulateJSON: true})
        .then(function (data) {
          if (!data.data.success) {
            that.Username = "未登录";
          }else{
            that.Username = data.data.entity.loginName;
            that.avatarUrl = data.data.entity.picImg==null?false:data.data.entity.picImgUrl;
          }
        })
    },
    mounted: function () {
    },
    components: {
      appHeaderBar:appHeader
    }
  }
</script>
