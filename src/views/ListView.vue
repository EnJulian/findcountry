<script setup xmlns="http://www.w3.org/1999/html">
import {onUpdated, ref} from "vue";
import axios from "axios";
import {useRouter} from "vue-router";
import Navigation from "@/components/Navigation.vue";
import LoadingState from "@/components/LoadingState.vue";

const router = useRouter();
const countries = ref([]);
const regions = ref([]);
const countryName = ref("");
const countryRegion = ref("");
const loading = ref(false)



function handleRegions(region){
  fetchRegionData(region)
}
async function fetchRegionData(fillRegion){
  try {
    loading.value = true;
    const response = await axios.get("https://restcountries.com/v3.1/region/" + fillRegion )
    countries.value = response.data
    loading.value = false;
  }
  catch (error){
    console.log(error)
    loading.value = false;
  }
}



async function fetchData(){
  try {
    // loading.value = true;
    const response = await axios.get("https://restcountries.com/v3.1/name/" + countryName.value )
    countries.value = response.data
    // loading.value = false;
  }
  catch (error){
    console.log(error)
    // loading.value = false;
  }
}
fetchData();
onUpdated(()=>{if (countryName.value !== ""){fetchData()} })


async function fetchAllData(){
  try {
    loading.value = true;
    const response = await axios.get("https://restcountries.com/v3.1/all" )
    countries.value = response.data
    loading.value = false;
  }
  catch (error){
    console.log(error)
    loading.value = false     ;
  }
}
fetchAllData();

</script>

<template>
  <div class="all">

      <div>
        <Navigation/>
      </div>
      
      <main class="box">
        <div class="search-n-filter">
          <div class="search-box">
            <span>&#128269;</span>
          <input v-model="countryName" type="text" placeholder="Search for a country... ">
          </div>
          
          <div class="filter-box">
            <ul>
              <li><a href="">Filter by Region &#9662;</a>
                <div class="dropdown">
                  <ul >
                    <li @click="handleRegions('Africa' )" >Africa</li>
                    <li @click="handleRegions( 'America' )" >America</li>
                    <li @click="handleRegions( 'Asia' )" >Asia</li>
                    <li @click="handleRegions( 'Europe' )" >Europe</li>
                    <li @click="handleRegions( 'Oceania' )" >Oceania</li>
                  </ul>
                </div>
              </li>
            </ul>
          </div>
        </div>
        <div class="loading-icon"><LoadingState v-if="loading"/></div>
       
        <div class="card-out">
          <div @click="router.push({name:'country', params:{name:country?.name.common}})" v-for="country in countries" class="card-in">
            <img :src="country?.flags.png" alt="pic">
            <div class="card-text">
              <p class="card-title"> {{ country?.name.common }} </p>
              <p>Population: {{country?.population}} </p>
              <p>Region: {{country?.region}} </p>
              <p>Capital: {{country?.capital?.[0]}} </p>
            </div>
          </div>
          
        </div>
      </main>
  </div>
</template>

<style scoped>

.box{
  background-color: #FAFAFA;
  padding: 48px 78px 900px 78px;
}
.search-n-filter{
 display: flex;
  justify-content: space-between;
}
.search-box{
  height: 25px;
  width: 200px;
  padding: 10px 200px 10px 20px;
  border-radius: 5px;
  background: #FFF;
  box-shadow: 0px 2px 9px 0px rgba(0, 0, 0, 0.05);
}
input{
  border: none;
}
input:focus {
  outline: none; 
  border: none; 
}
.filter-box{
  
  text-align: center;
}
.filter-box ul{
  box-shadow: 0 2px 9px -9px rgba(0, 0, 0, 0.08);
  list-style: none;
  
}
.filter-box ul li{
  
  background-color: white;
  color: black;
  padding:15px;
}
.filter-box ul li:hover{
  background: #FFFFFF;
  color: black;
}
.filter-box ul li a{
  text-decoration: none;
}
.dropdown{
  display: none;
}

.loading-icon{
  display: flex;
  justify-content: center;
}

.filter-box ul li:hover .dropdown{
  box-shadow: 0px 2px 9px 0px rgba(0, 0, 0, 0.05);
  display: block;
  position: absolute;
  background: #FFFFFF;
  margin-top: 15px;
  margin-left: -15px;
}
.filter-box ul li:hover .dropdown li{
  margin-right: 30px;
  
}
.card-out{
  display: grid;
  grid-template-columns: repeat(4, 1fr);
}
.card-in{
  border-radius: 5px;
  background: #FFF;
  box-shadow: 0px 0px 7px 2px rgba(0, 0, 0, 0.03);
  width: 264px;
  height: 336px;
  flex-shrink: 0;
  margin-bottom: 50px;
}
.card-in img{
  height: 150px;
  width: 100%;
}
.card-text{
  padding: 0 30px;
}
.card-title{
  color: #111517;
  font-family: Nunito Sans;
  font-size: 18px;
  font-style: normal;
  font-weight: 800;
  line-height: 26px; /* 144.444% */
}

</style>
