<script setup>
import {useRouter} from "vue-router";
import {useRoute} from "vue-router";
import axios from "axios";
import {computed, ref} from "vue";
import Navigation from "@/components/Navigation.vue";  

const route = useRoute();
const router = useRouter();
const countries = ref([]);
console.log(route.params.name)
async function fetchData(){
  try {
    const response = await axios.get("https://restcountries.com/v3.1/name/" + route.params.name )
    countries.value = response.data
  }
  catch (error){
    console.log(error)
  }
}
fetchData();
</script>

<template>
  <div>
    <Navigation/>
  </div>
  
  <div @click="router.back" class="back-button">
    <p>&#8592;    Back</p>
  </div>
  
  <div class="bottom-section">
    <img :src="countries[0]?.flags.png" alt="">
    
    <div class="bottom-right">
      <h1>{{countries[0]?.name.common}}</h1>
      
      <div class="bottom-tags">
        <div class="tags-left">
          <p><strong>Native Name:</strong> <span v-for="nativeName in countries[0]?.name.nativeName">  {{nativeName.official}},  </span></p>
          <p><strong>Population:</strong> {{countries[0]?.population}} </p>
          <p><strong>Region: </strong> {{countries[0]?.region}} </p>
          <p><strong>Sub Region:</strong> {{countries[0]?.subregion}} </p>
          <p><strong>Capital:</strong> {{countries[0]?.capital?.[0]}}</p>
        </div>
        
        <div class="tags-right">
          <p> <strong>Top Level Domain:</strong> {{countries[0]?.tld?.[0]}} </p>
          <p><strong>Currencies:</strong>  <span v-for="currencyName in countries[0]?.currencies">  {{currencyName.name}}  </span> </p>
          <p><strong>Languages:</strong> <span v-for="languageName in countries[0]?.languages">  {{languageName}},  </span> </p>
        </div>
      </div>
      
    </div>
    
  </div>
  
  
</template>
<style scoped>
.back-button{
  margin: 80px 0 0 100px;
  width: 100px;
}

.bottom-section{
  display: flex;
  padding: 80px 80px;
  gap: 120px;
}
img{
  width: 560px;
  height: 401px;
}
.bottom-tags{
  display: flex;
  gap: 141px;
}
</style>
