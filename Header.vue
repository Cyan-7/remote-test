<script setup>
import router from '../routers/router';
import { isLogin } from '../store/userStore';

const loginState = isLogin()

function logout(){
    loginState.changeLoginUser(null)
    if(loginState.changeLoginUser === null){
        localStorage.setItem("isLogin","-1")
    }
    router.push("/login")
}

</script>

<template>
  <div class="header">
    <h1>日程管理系统</h1>
    

    <div class="headerDIV" v-if="loginState.getLoginUser !== null">
        <span class="left">
            <button @click="logout()">退出登录</button>
        </span>
        <span class="right">
            <router-link to="/showSchedule">
            <button>查看我的日程</button>
            </router-link>
        </span>
    </div>

    <div class="headerDIV" v-else>
        <span class="left">
            <router-link to="/login">
            <button>登录</button>
            </router-link>
        </span>
        
        <span class="right">
            <router-link to="/regist">
            <button>注册</button>
            </router-link>
        </span>

        <!-- <span class="right">
            <router-link to="/homework">
            <button>作业</button>
            </router-link>
        </span> -->
    </div>
  </div>
</template>

<style scoped>
    .header{
        margin-bottom: 0.9em;
    }

    .header .headerDIV{
        display: flex;
        margin-top: 0.4em;
        padding-left: 55%;
    }

    .header .headerDIV .left,
    .header .headerDIV .right{
        margin-right: 10px;
    }
</style>
