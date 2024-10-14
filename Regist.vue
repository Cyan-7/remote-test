<script setup>
import router from "../routers/router";
import {reactive, ref} from "vue"
import request from "../utils/request"

// 包含 用户名、用户密码
const registUser = reactive({
    userName:"",
    userPwd:"",
})


// 用户输入的 “确认密码”
let reUserPwd = ref("")
// 用于反应用户输入格式是否正确
let userNameMsg = ref("")
let userPwdMsg = ref("")
let reUserPwdMsg = ref("")

function goLogin(){
    router.push("/login")
}

async function saveRegist(){

        if(checkuserName() && checkUserPwd() && checkReUserPwd()){
        let {data} = await request.post("user/register",registUser)
        
        if(data.code === 200){
            alert("注册成功")
        }else{
            alert("注册失败")
        }
        router.push("/login")
    }
}


async function checkuserName(){
    // 定义正则
    let userNameReg=/^[a-zA-Z0-9]{5,10}$/
    // 校验
    if(!userNameReg.test(registUser.userName)){
        // 提示
        userNameMsg.value = "格式有误"
        return false
    }

    let {data} =await request.post(`user/checkUserUsed?userName=${registUser.userName}`)
    
    if(data.code !== 200){
        userNameMsg.value = "账号已存在"
        return false
    }
    
    // 通过校验
    userNameMsg.value="可用"
    return true
}
        // 校验密码的方法
function checkUserPwd(){
    // 定义正则
    let passwordReg=/^[0-9]{6}$/
        // 校验
        if(!passwordReg.test(registUser.userPwd)){
        // 提示
        userPwdMsg.value = "格式有误"
        return false
    }
    // 通过校验
    userPwdMsg.value="可用"
    return true
}
        // 校验密码的方法
function checkReUserPwd(){
    // 定义正则
    let passwordReg=/^[0-9]{6}$/
    // 校验
    if(!passwordReg.test(reUserPwd.value)){
        // 提示
        reUserPwdMsg.value = "格式有误"
        return false
    }
    // 校验
    if(!(registUser.userPwd==reUserPwd.value)){
        // 提示
        reUserPwdMsg.value = "输入不一致"
        return false
    }


    // 通过校验
    reUserPwdMsg.value="可用"
    return true
}

function reset(){
    registUser.userName = ""
    registUser.userPwd = ""
    reUserPwd.value = ""
    userNameMsg.value = ""
    userPwdMsg.value = ""
    reUserPwdMsg.value = "" 
}
</script>

<template>
    <div class="regist">
        <h1>注册</h1>
        <div class="table">
            <ul>
                <li>
                    <span class="left">
                        输入账号:
                    </span>
                    <span class="middle">
                        <input type="text" v-model="registUser.userName" @blur="checkuserName()">
                    </span>
                    <span class="right">{{ userNameMsg }}</span>
                </li>
                <li>
                    <span class="left">
                        输入密码:
                    </span>
                    <span class="middle">
                        <input type="password" v-model="registUser.userPwd" @blur="checkUserPwd()">
                    </span>
                    <span class="right">{{ userPwdMsg }}</span>
                </li>
                <li>
                    <span class="left">
                        确认密码:
                    </span>
                    <span class="middle">
                        <input type="password" v-model="reUserPwd" @blur="checkReUserPwd()">
                    </span>
                    <span class="right">{{ reUserPwdMsg }}</span>
                </li>
                <li>
                    <button @click="saveRegist()">注册</button>
                    <button @click="reset()">重置</button>
                    <button @click="goLogin()">去登录</button>
                </li>
            </ul>
        </div>
    </div>
</template>

<style scoped>
.regist h1{
    margin-top: 0.3em;
}

.regist .table{
    height: 10em;
}

.regist .table ul li{
    height: 25%;
}

.regist .table ul li:nth-child(4){
    align-items: center;
    justify-content: center;
}

.regist .table ul li:nth-child(4) button{
    margin-left: 0.9em;
}
</style>
