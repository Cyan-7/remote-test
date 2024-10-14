<script setup>
import router from "../routers/router";
import {reactive, ref} from "vue"
import request from "../utils/request"

// 包含 用户名、用户密码
const registUser = reactive({
    userName:"",
    userAge:"",
    userEmail:""
})

async function saveRegist(){       
    let {data} = await request.post("user/homework",registUser)

    if(data !== null){
        alert("注册成功")
    }
}

</script>

<template>
  <div class="regist">
        <h1>作业</h1>
        <div class="table">
            <ul>
                <li>
                    <span class="left">
                        姓名:
                    </span>
                    <span class="middle">
                        <input type="text" v-model="registUser.userName">
                    </span>
                    <span class="right"></span>
                </li>
                <li>
                    <span class="left">
                        年龄:
                    </span>
                    <span class="middle">
                        <input type="text" v-model="registUser.userAge">
                    </span>
                    <span class="right"></span>
                </li>
                <li>
                    <span class="left">
                        邮箱:
                    </span>
                    <span class="middle">
                        <input type="text" v-model="registUser.userEmail">
                    </span>
                    <span class="right"></span>
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
