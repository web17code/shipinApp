<style scoped>
  /**
  * Created by web17code
  */
  /*navbar bymyself*/
  .NavContent {
    padding: 0 0.5rem;
    height: 3rem;
    background-color: #2196f3;
    display: flex;
    flex-direction: row;
    align-items: center; /*次轴对齐方式*/
    justify-content: space-between; /*主轴对齐方式*/
    color: #fff;
    align-content: space-between;
    box-shadow: 0 1px 6px rgba(0, 0, 0, .117647), 0 1px 4px rgba(0, 0, 0, .117647);
  }

  .isHide {
    visibility: hidden;
  }

  .NavRight {
    display: flex;
    font-size: 1.6rem;
    padding-left: 0.5rem;
  }

  .NavLeft {
    display: flex;
    padding-right: 0.5rem;
  }

  .NavCenter {
    display: flex;
    color: #fff;
    line-height: 2.2rem;
    height: 2.2rem;
    font-size: 1rem;
  }

  .NavCenter p {
    display: inline-block;
    text-align: center;

  }

  /*navbar bymyself*/

</style>

<template>
  <div class="NavContent">
    <img src="../assets/ic_navigate_before_wirte_24px.svg"
         @click="goBack"
         :class="[{ 'isHide': isHideLeft }, 'NavLeft']"
         alt="">
    <p class="NavCenter"
       style="display: block;text-align: center;">{{text}}</p>
    <img src="../assets/ic_search_wirte_24px.svg"
         @click="goSearch"
         :class="[{'isHide':isHideRight},'NavRight']"
         alt="">
  </div>
</template>

<script>
  export default {
    data: function () {
      return {}
    },
    props: {
      text: "",
      isHideLeft: {
        type: Boolean,
        default:true
      },
      isHideRight: {
        type: Boolean,
        default:true
      }
    },
    methods: {
      goSearch: function () {
        this.$router.push(
          //, query: {user: "zhuhj"}
          {path: "search_nobar", query: {}})
      },
      goBack: function () {
        this.$router.go(-1)
      }
    },
    created: function () {
    },
    mounted: function () {

    },
    components: {}
  }
</script>
