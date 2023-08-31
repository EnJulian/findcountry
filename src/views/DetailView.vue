<script setup>
import {useRouter} from "vue-router";
import {useRoute} from "vue-router";
import axios from "axios";
import {computed, ref} from "vue";  

const route = useRoute();
const router = useRouter();
const meals = ref([]);
async function fetchData(){
  try {
    const response = await axios.get("https://themealdb.com/api/json/v1/1/search.php?s=" + route.params.name )
    meals.value = response.data.meals
  }
  catch (error){
    console.log(error)
  }
}
fetchData();
const instructions = computed(()=>{return meals.value[0].strInstructions.split("\r\n")})
</script>

<template>
  
  <div class="detail-view">
    <div class="div">
      <div class="overlap">
        <div class="group"></div>
        <img class="unsplash" :src="meals[0].strMealThumb" />
        <div class="group-2"></div>
        <div  @click="router.push({name:'home'})" class="text-wrapper">Home</div>
        <div @click="router.push({name:'search'})" class="text-wrapper-2">Search</div>
        <div class="text-wrapper-3">{{ meals[0].strMeal }}</div>
        <div class="frame">
          <div class="frame-2">
            <div class="frame-3">
              <img class="img" src="src/assets/bxs_category.png"  alt=""/>
              <div class="text-wrapper-4">CATEGORY</div>
            </div>
            <div class="text-wrapper-5">Chicken</div>
          </div>
          <div class="frame-2">
            <div class="frame-4">
              <div class="frame-5">
                <img class="img" src="src/assets/ci_location.svg"  alt=""/>
                <div class="text-wrapper-4">AREA</div>
              </div>
              <div class="text-wrapper-5">Japanese</div>
            </div>
          </div>
          <div class="frame-2">
            <div class="frame-3">
              <img class="img" src="src/assets/fa6-solid_tags.svg"  alt=""/>
              <div class="text-wrapper-4">TAGS</div>
            </div>
            <div class="text-wrapper-5">{{ meals[0].strTags }}</div>
          </div>
        </div>
      </div>
      <div class="text-wrapper-6">Instructions</div>
      <div class="overlap-group-wrapper">
        <div class="overlap-group">
          <div class="text-wrapper-7">Ingredients</div>
          <div class="frame-6">
            <div class="text-wrapper-8">Soy Sauce</div>
            <div class="element-cup-wrapper"><div class="element-cup">3/4 Cup</div></div>
          </div>
          <div class="overlap-2">
            <div class="frame-7">
              <div class="text-wrapper-9">Minced Garlic</div>
              <div class="element-teaspoon-wrapper"><div class="element-teaspoon">1/2 Teaspoon</div></div>
            </div>
          </div>
          <div class="div-wrapper"><div class="text-wrapper-8">Water</div></div>
          <div class="frame-8"><div class="text-wrapper-8">Brown Sugar</div></div>
          <div class="stir-fry-vegetables-wrapper"><div class="text-wrapper-8">Stir-fry Vegetables</div></div>
        </div>
      </div>
      <div  class="instructions" v-for="instruction in instructions">{{ instructions }}
     
      </div>
    </div>
  </div>
</template>
<style scoped>
.detail-view {
  background-color: #f8f8f8;
  display: flex;
  flex-direction: row;
  justify-content: center;
  width: 100%;
  
}

.detail-view .div {
  background-color: #f8f8f8;
  width: 100%;
  height: 1024px;
  position: relative;
  padding-bottom: 500px;
}

.detail-view .overlap {
  position: absolute;
  width: 100%;
  height: 441px;
  top: 0;
  left: 0;
}

.detail-view .group {
  position: absolute;
  width: 100%;
  height: 347px;
  top: 0;
  left: 0;
  background-color: #ff9e59;
  box-shadow: inset 0px -24px 32px -28px #c0560966;
  background-size: 100% 100%;
}

.detail-view .unsplash {
  position: absolute;
  width: 324px;
  height: 305px;
  top: 136px;
  left: 290px;
}

.detail-view .group-2 {
  position: absolute;
  width: 112px;
    height: 48px;
  top: 19px;
  left: 120px;
  background-size: 100% 100%;
}

.detail-view .text-wrapper {
  position: absolute;
  cursor: pointer;
  top: 30px;
  left: 86%;
  font-family: "IBM Plex Sans-Regular", Helvetica;
  font-weight: 400;
  color: #000000;
  font-size: 18px;
  letter-spacing: 0;
  line-height: 23.4px;
  white-space: nowrap;
}

.detail-view .text-wrapper-2 {
  position: absolute;
  cursor: pointer;
  top: 30px;
  left: 90%;
  font-family: "IBM Plex Sans-Bold", Helvetica;
  font-weight: 700;
  color: #000000;
  font-size: 18px;
  letter-spacing: -0.72px;
  line-height: 23.4px;
  white-space: nowrap;
}

.detail-view .text-wrapper-3 {
  position: absolute;
  top: 168px;
  left: 622px;
  font-family: "IBM Plex Sans-Bold", Helvetica;
  font-weight: 700;
  color: #000000;
  font-size: 40px;
  letter-spacing: -0.8px;
  line-height: 40px;
  white-space: nowrap;
}

.detail-view .frame {
  display: inline-flex;
  align-items: flex-start;
  gap: 16px;
  position: absolute;
  top: 233px;
  left: 622px;
}

.detail-view .frame-2 {
  display: inline-flex;
  flex-direction: column;
  align-items: flex-start;
  gap: 8px;
  padding: 12px 24px;
  position: relative;
  flex: 0 0 auto;
  background-color: #ffffff4c;
  border-radius: 4px;
  box-shadow: inset 1px 1px 2px #ffffff5e, 0px 8px 8px #0000000d;
  backdrop-filter: blur(94px) brightness(100%);
  -webkit-backdrop-filter: blur(94px) brightness(100%);
}

.detail-view .frame-3 {
  display: inline-flex;
  align-items: center;
  gap: 4px;
  position: relative;
  flex: 0 0 auto;
}

.detail-view .img {
  position: relative;
  width: 16px;
  height: 16px;
}

.detail-view .text-wrapper-4 {
  position: relative;
  width: fit-content;
  font-family: "IBM Plex Sans-Regular", Helvetica;
  font-weight: 400;
  color: #944f1c;
  font-size: 10px;
  letter-spacing: 0.9px;
  line-height: 10px;
  white-space: nowrap;
}

.detail-view .text-wrapper-5 {
  color: #000000;
  font-size: 20px;
  letter-spacing: -0.4px;
  line-height: 20px;
  position: relative;
  width: fit-content;
  font-family: "IBM Plex Sans-Regular", Helvetica;
  font-weight: 400;
  white-space: nowrap;
}

.detail-view .frame-4 {
  display: inline-flex;
  flex-direction: column;
  align-items: flex-start;
  gap: 8px;
  position: relative;
  flex: 0 0 auto;
}

.detail-view .frame-5 {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 4px;
  position: relative;
  flex: 0 0 auto;
}

.detail-view .text-wrapper-6 {
  position: absolute;
  top: 759px;
  left: 425px;
  font-family: "IBM Plex Sans-Bold", Helvetica;
  font-weight: 700;
  color: #000000;
  font-size: 32px;
  letter-spacing: -0.64px;
  line-height: 32px;
  white-space: nowrap;
}

.detail-view .overlap-group-wrapper {
  position: absolute;
  width: 592px;
  height: 219px;
  top: 469px;
  left: 425px;
}

.detail-view .overlap-group {
  position: relative;
  width: 590px;
  height: 219px;
  background-color: #ffffff99;
  border-radius: 10px;
  box-shadow: 0px 24px 64px -16px #0000001a, inset 0px 4px 2px #ffffffa6;
  backdrop-filter: blur(24px) brightness(100%);
  -webkit-backdrop-filter: blur(24px) brightness(100%);
}

.detail-view .text-wrapper-7 {
  position: absolute;
  top: 27px;
  left: 32px;
  font-family: "IBM Plex Sans-Bold", Helvetica;
  font-weight: 700;
  color: #000000;
  font-size: 32px;
  letter-spacing: -0.64px;
  line-height: 32px;
  white-space: nowrap;
}

.detail-view .frame-6 {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  padding: 8px 16px;
  position: absolute;
  top: 91px;
  left: 33px;
  border-radius: 30px;
  border: 1px solid;
  border-color: #909090;
}
.detail-view .frame-6:hover{
  background-color: #ff9f59;
  box-shadow: 0px 4px 14px #f98a3a66, inset 1px 2px 2px #ffffff4a;
  color: black;
}

.detail-view .text-wrapper-8 {
  position: relative;
  width: fit-content;
  margin-top: -0.5px;
  font-family: "IBM Plex Sans-Regular", Helvetica;
  font-weight: 400;
  color: #000000;
  font-size: 16px;
  letter-spacing: 0;
  line-height: 16px;
  white-space: nowrap;
}

.detail-view .text-wrapper-8:hover{
  color: black;
}

.detail-view .element-cup-wrapper {
  display: inline-flex;
  align-items: flex-start;
  gap: 10px;
  padding: 2px 8px;
  position: relative;
  flex: 0 0 auto;
  background-color: #aaaaaa;
  border-radius: 30px;
}

.detail-view .element-cup {
  position: relative;
  width: fit-content;
  margin-top: -1px;
  font-family: "IBM Plex Sans-Regular", Helvetica;
  font-weight: 400;
  color: #ffffff;
  font-size: 12px;
  letter-spacing: 0;
  line-height: 12.6px;
  white-space: nowrap;
}

.detail-view .overlap-2 {
  position: absolute;
  width: 230px;
  height: 50px;
  top: 142px;
  left: 33px;
}

.detail-view .frame-7 {
  display: flex;
  width: 230px;
  height: 38px;
  align-items: center;
  gap: 10px;
  padding: 8px 16px;
  position: absolute;
  top: 0;
  left: 0;
 
  border-radius: 30px;
  border: 1px solid;
 
}
.detail-view .frame-7:hover{
  background-color: #ff9f59;
  box-shadow: 0px 4px 14px #f98a3a66, inset 1px 2px 2px #ffffff4a;
  color: black;
}

.detail-view .text-wrapper-9 {
  position: relative;
  width: fit-content;
  font-family: "IBM Plex Sans-Regular", Helvetica;
  font-weight: 400;
  color: #000000;
  font-size: 16px;
  letter-spacing: 0;
  line-height: 16px;
  white-space: nowrap;
}

.detail-view .element-teaspoon-wrapper {
  display: inline-flex;
  align-items: flex-start;
  gap: 10px;
  padding: 2px 8px;
  position: relative;
  flex: 0 0 auto;
  background-color: #ffffff;
  border-radius: 30px;
}

.detail-view .element-teaspoon {
  position: relative;
  width: fit-content;
  margin-top: -1px;
  font-family: "IBM Plex Sans-Regular", Helvetica;
  font-weight: 400;
  color: #ff9f59;
  font-size: 12px;
  letter-spacing: 0;
  line-height: 12.6px;
  white-space: nowrap;
}

.detail-view .bi-hand-index-thumb {
  position: absolute;
  width: 16px;
  height: 16px;
  top: 34px;
  left: 19px;
}

.detail-view .div-wrapper {
  display: inline-flex;
  height: 33px;
  align-items: center;
  gap: 10px;
  padding: 8px 16px;
  position: absolute;
  top: 91px;
  left: 225px;
  border-radius: 30px;
  border: 1px solid;
  border-color: #909090;
}
.detail-view .div-wrapper:hover{
  background-color: #ff9f59;
  box-shadow: 0px 4px 14px #f98a3a66, inset 1px 2px 2px #ffffff4a;
  color: black;
}

.detail-view .frame-8 {
  display: inline-flex;
  height: 33px;
  align-items: center;
  gap: 10px;
  padding: 8px 16px;
  position: absolute;
  top: 91px;
  left: 316px;
  border-radius: 30px;
  border: 1px solid;
  border-color: #909090;
}
.detail-view .frame-8:hover{
  background-color: #ff9f59;
  box-shadow: 0px 4px 14px #f98a3a66, inset 1px 2px 2px #ffffff4a;
  color: black;
}

.detail-view .stir-fry-vegetables-wrapper {
  display: inline-flex;
  height: 33px;
  align-items: center;
  gap: 10px;
  padding: 8px 16px;
  position: absolute;
  top: 148px;
  left: 300px;
  border-radius: 30px;
  border: 1px solid;
  border-color: #909090;
}
.detail-view .stir-fry-vegetables-wrapper:hover{
  background-color: #ff9f59;
  box-shadow: 0px 4px 14px #f98a3a66, inset 1px 2px 2px #ffffff4a;
  color: black;
}

.detail-view .instructions {
  position: absolute;
  top: 823px;
  left: 19%;
  font-family: "IBM Plex Sans-Regular", Helvetica;
  font-weight: 200;
  color: #000000;
  font-size: 16px;
  letter-spacing: 0;
  line-height: 26.4px;
  
}

</style>
