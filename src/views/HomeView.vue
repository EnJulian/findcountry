<script setup>
import {onUpdated, ref} from "vue";
import {useRouter} from "vue-router";

const router = useRouter();
const meals = ref([]);
const mealName = ref("");
</script>

<template>
 
  <div class="home">
    <div class="overlap-wrapper">
      <div class="overlap">
        
        <div class="rectangle"></div>
        <div class="group"></div>
        <p class="page-header">Find recipes for the ingredients you have on hand</p>
        <img class="image" src="src/assets/image-1.png" />
        <div class="search-div">
          <div @click="router.push({name:'search'})" class="search-button"><div class="div">Search Now</div></div>
        </div>
        <nav class="nav-bar">
          <img class="foodl" src="src/assets/foodl.svg" alt="">
          <span class="nav-item-right">Home</span>
          <span  @click="router.push({name:'search'})" class="nav-item-right">Search</span>
        </nav>
      </div>
    </div>
  </div>

</template>

<style>
.home {
  
  display: flex;
  flex-direction: row;
  justify-content: center;
  width: 100%;
}

.home .overlap-wrapper {
  background-color: #FF9F59;
  width: 100%;
  height: 1024px;
}

.home .overlap {
  position: relative;
  height: 1024px;
}

.home .frame {
  position: absolute;
  width: 100%;
  height: 1024px;
  top: 0;
  left: 0;
  background-color: #ff9e59;
  box-shadow: inset 0px -24px 32px -28px #c0560966;
}

.home .noise {
  position: absolute;
  width: 100%;
  height: 1px;
  top: 1024px;
  left: 0;
}

.nav-bar{
  position: absolute;
  top: 30px;
  left: 10%;
}
nav img{
  margin-right: 1500px;
}
nav span{
  margin: auto 20px;
  font-family: "IBM Plex Sans-Bold", Helvetica;
  font-weight: 700;
  color: #000000;
  cursor: pointer;
  font-size: 18px;
  letter-spacing: -0.72px;
  line-height: 23.4px;
  white-space: nowrap;
}


.home .rectangle {
  position: absolute;
  width: 392px;
  height: 151px;
  top: 378px;
  left: 83%;
  background-color: #000000;
}

.home .group {
  width: 112px;
  height: 48px;
  top: 19px;
  background-image: url(./img/subtract.svg);
  background-size: 100% 100%;
  position: absolute;
  left: 120px;
}

.home .page-header {
  position: absolute;
  width: 442px;
  top: 280px;
  left: 15%;
  font-family: "IBM Plex Sans-Bold", Helvetica;
  font-weight: 700;
  color: #000000;
  font-size: 48px;
  letter-spacing: -1.92px;
  line-height: 62.4px;
}

.home .image {
  position: absolute;
  width: 619px;
  height: 640px;
  top: 161px;
  left: 65%;
  object-fit: cover;
}

.home .search-div {
  width: 246px;
  height: 72px;
  top: 560px;
  position: absolute;
  left: 15%;
}

.home .search-button {
  cursor: pointer;
  position: relative;
  width: 244px;
  height: 72px;
  background-color: #000000;
  border-radius: 8px;
  box-shadow: 0px 16px 40px #c0560966;
}

.home .div {
  top: 20px;
  left: 60px;
  font-family: "IBM Plex Sans-Medium", Helvetica;
  font-weight: 500;
  color: #ffffff;
  font-size: 24px;
  letter-spacing: -0.96px;
  line-height: 31.2px;
  position: absolute;
  white-space: nowrap;
}



</style>
