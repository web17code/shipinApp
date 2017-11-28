<style scoped>
    /**
    * Created by web17code
    */
    .visionC{
      display: flex;
      flex-direction: column;
      justify-content: center;
      height: 90vh;
    }
    .visionC p{
      font-size: 1rem;
    }
</style>

<template>
  <div>
    <!--标题-->
    <appHeaderBar text="关于" :isHideLeft="false" :isHideRight="true"></appHeaderBar>
    <div class="visionC">
      <p>上海市生物资源建设项目移动终端应用系统 V1.0</p>
    </div>
  </div>
</template>

<script>
    import appHeader from "../components/appHeader.vue"
    export default {
        data: function () {
            return {}
        },
        props: {},
        methods: {},
        created: function () {
        },
        mounted: function () {
        },
        components: {
          appHeaderBar:appHeader
        }
    }
</script>
