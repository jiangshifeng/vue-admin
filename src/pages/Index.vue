<template>
    <div id="index" class="flex-col">
      <div id="head" style="justify-content: space-between" class="flex-row">
        <div class="flex-align" style="height: 64px;margin-left: 40px">
          <Icon type="ios-chatboxes" size="50" color="white"></Icon>
          <div class="flex-align" style="height: 64px;color: white;font-size: 16px;margin-left: 20px;letter-spacing: 2px">
            V商城管理系统
          </div>
        </div>
        <div style="height: 64px;margin-right: 40px" class="flex-align flex-row">
          <span style="color: white;margin-right: 20px"> 欢迎你,<router-link to="/"><span style="color: white;cursor: pointer">{{reqData.roleName}}</span></router-link></span>
          <Poptip
            confirm
            placement="bottom-end"
            title="要退出登录吗？"
            @on-ok="loginOut"
            @on-cancel="">
          <Icon type="log-out" size="20" color="white" style="cursor: pointer" title="退出登录"></Icon>
          </Poptip>
        </div>
      </div>
      <div style="flex: 1" class="flex-row">
        <div id="navMenu">
          <nav-menu></nav-menu>
        </div>
        <router-view style="flex: 1;background-color: #faf7fa;overflow: auto" />
      </div>
    </div>
</template>

<script>
  import navMenu from "@/components/nav/navMenu"

    export default {
      name: "index",
      data(){
        return{
          reqData:{
            roleName:"杨坤凡"
          }
        }
      },
      methods:{
        loginOut(){
          this.$router.push({path:"/"})
        }
      },
      components:{
        navMenu
      }
    }
</script>
<style lang="less">
  #index{
    width: 100%;
    height: 100%;
      #head{
        height: 64px;
        background-color: #08a2ba;
      }
  }
  #navMenu{
    height: calc(100vh-64 px);
    overflow: auto;
    background-color: #495060;
  }
</style>
<style scoped lang="less">
  #index{

  }
</style>
