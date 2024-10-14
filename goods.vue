<script setup>
import {goodsInfo} from "../store/goodsInfo"
const info = goodsInfo()
function addGoods(){  
}

function deleteGoods(index){
    //如果用于存放商品信息得数组不为空就删除
    if(info.getGoodsInfo !== null){
        info.deleteGoods(index)
    }
}

//用于存放输入的标签内容
let tagContent = ""
function addTag(index){
    // 判断输入是否为空
    if (tagContent.trim()) {
        // 将输入的内容添加到对应商品的 tags 数组中
        info.Info[index].tags.push(tagContent);
        tagContent = ""
    }
}
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
            <li v-for="(goodsInfo,index) in info.getGoodsInfo" :key="index">
                <div class="id">{{ goodsInfo.id }}</div>
                <div class="name">{{ goodsInfo.name }}</div>
                <div class="price">{{ goodsInfo.price }}</div>
                <div class="tag tag2">
                    <input type="text" class="addTag" placeholder="+Tag" @blur="addTag(index)" v-model="tagContent"> <!-- 传入当前 li 标签的 index -->
                    <div class="tagList">
                        <button class="tagContent" v-for="(tag,index) in goodsInfo.tags" :key="index">{{ tag }}</button>
                    </div>
                </div>
                <div class="action">
                    <!-- 传入当前 li 标签的 index -->
                    <button @click="deleteGoods(index)">删除</button>
                </div>
            </li>
            <button class="addGoods" @click="addGoods()">添加商品</button>
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
