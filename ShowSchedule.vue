<script setup>
import { ref } from 'vue';
import { isLogin } from "../store/userStore";

const loginState = isLogin()

let username = ref(loginState.getLoginUser)
</script>

<template>
    <div class="table">
        <ul>
            <li>
                <div class="id">ID</div>
                <div class="name">商品名称</div>
                <div class="price">价格</div>
                <div class="tag">标签</div>
                <div class="action">操作</div>
            </li>
            <!-- 根据 存放商品信息的数组长度渲染 li 标签-->
            <li >
                <div class="id"></div>
                <div class="name"></div>
                <div class="price"></div>
                <div class="tag tag2">
                    <input type="text" class="addTag" placeholder="+Tag"> <!-- 传入当前 li 标签的 index -->
                    <div class="tagList">
                        <button class="tagContent" ></button>
                    </div>
                </div>
                <div class="action">
                    <!-- 传入当前 li 标签的 index -->
                    <button >删除</button>
                </div>
            </li>
            <button class="addGoods" >添加商品</button>
        </ul>
    </div>
</template>

<style scoped>
.table{
  margin: 0 auto;
  margin-top: 0.8em;
  min-width: 100%;
  border-radius: 10px;
  box-shadow: 0.5px 0.5px 5px gray;
}

.table li div{
    border: 1px,solid,lightgray;
    border-right: none;
    border-left: none;
    display: flex;
    justify-content: center;
    align-items: center;
}

.table .addGoods{
    margin: 0.5vh auto;
}

.table ul{
  height: 100%;
  list-style-type: none;
  padding: 0; /* 可选，去掉内边距 */
  margin: 0;  /* 可选，去掉外边距 */
}

.table ul li{
  display: flex;
  width: 100%;
  min-height: 5vh;
  /* border: 1px,solid,black; */
}

.table .id{
    min-width: 4%;
}

.table .name{
    min-width: 48%;
}

.table .price{
    min-width: 8%;
}

.table .tag,
.table .tag2{
    min-width: 32%;
}

.table .tag2{
    justify-content:flex-start
}

.table .tag .addTag{
    margin-left: 2vw;
    margin-right: 0.5vw;
    max-width: 3.5vw;
    max-height: 3vh;
    background-color: #F0F0F0;
    font-size: 12px;
}

.table .tag .tagList{
    border: none;
}

.table .tag .tagList .tagContent{
    margin-right: 0.3vw;
    font-size: 13px;
    font-weight: 500;
    font-family: inherit;
    min-width: 3vw;
    padding: 0.1em 0.2em;
}

.table .action{
    min-width: 8%;
}
</style>
