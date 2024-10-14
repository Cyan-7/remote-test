<script setup>
import {reactive, ref} from "vue"
import router from "../routers/router"
import request from "../utils/request"
import { isLogin } from "../store/userStore";

const loginState = isLogin()

// 包含 用户名、用户密码
const registUser = reactive({
    userName:"",
    userPwd:"",
})

let usernameMsg = ref("")
let userPwdMsg = ref("")

async function login(){
    let {data} = await request.post("user/login",registUser)
    
    if(data.code === 200){
        loginState.changeLoginUser(registUser.userName)
        router.push("/showSchedule")
    }else if(data.code === 501){
        usernameMsg.value = "没有这个账号"
    }else if(data.code === 503){
        userPwdMsg.value = "密码错误"
    }
}

function reset(){
    registUser.userName = ""
    registUser.userPwd = ""
    usernameMsg.value = ""
    userPwdMsg.value = ""
}

function goRegist(){
    router.push("/regist")
}
</script>

<template>
     <div class="login">
        <h1>登录</h1>
        <div class="table">
            <ul>
                <li>
                    <span class="left">
                        输入账号:
                    </span>
                    <span class="middle">
                        <input type="text" v-model="registUser.userName">
                    </span>
                    <span class="right">{{ usernameMsg }}</span>
                </li>
                <li>
                    <span class="left">
                        输入密码:
                    </span>
                    <span class="middle">
                        <input type="password" v-model="registUser.userPwd">
                    </span>
                    <span class="right">{{ userPwdMsg }}</span>
                </li>
                <li>
                    <button @click="login()">登录</button>
                    <button @click="reset()">重置</button>
                    <button @click="goRegist()">去注册</button>
                </li>
            </ul>
        </div>
    </div>
</template>

<style scoped>
.login h1{
    margin-top: 0.3em;
}

.login .table{
    height: 8em;
}

.login .table ul li{
    height: 33%;
}

.login .table ul li:nth-child(3){
    align-items: center;
    justify-content: center;
}

.login .table ul li:nth-child(3) button{
    margin-left: 0.9em;
}
</style>