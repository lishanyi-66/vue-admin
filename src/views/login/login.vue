<template>
  <div class="login">
    <div class="loginbox">
      <div class="loginleft">
        <ul class="menu-tab">
          <li v-for='item in menuTab' :key='item.id'>{{item.text}}</li>
        </ul> 
      </div>
      <div class="loginright"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "login",
  data(){
    return {
      menuTab:[
        {text:'登录'},
        {text:'注册'}
      ]
        
      }
    }
  
};
</script>

<style lang="less" scoped>
.login{
  height: 100vh;
  background-color: #1282E0;
  display: flex;
  justify-content: center;
  align-items: center;
  .loginbox{
    width: 60vw;
    height: 400px;
    background-color: #fff;
    display: flex;
    .loginleft{
      flex: 5;
      .menu-tab{
        list-style: none;
        display: flex;
        font-size: 20px;
        li{
          padding: 20px;
        }
        
      }
    }
    .loginright{
      flex: 3;
      height: 100%;
      background-color: #4AA9F5;
    }
  }
}
</style>