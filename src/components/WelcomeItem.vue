<script setup>
import { data } from "./cars.json";
import {ref} from "vue"

const questions = ref(data)

const car = ref("car")
</script>

<template>
  

  <div class="container">
<div class="cards">
  <div class="card-container" v-for="question in questions" :key="question.id">
    <div class="card"  >
      <div class="image-container">
        <div class="image-item" v-for="image in question.media_urls[0]" :key="image">
            <!-- <p>{{ image }}</p> -->
          <img :src="image">
        </div>
      </div>
      <div class="content-container">
        <div class="content">{{ car }}</div>
      </div>
    </div>
  </div>
</div>
</div>
</template>

<style scoped>
img{
  height: 100%;
    -o-object-fit: cover;
    object-fit: cover;
    width: 100%;
    border-radius: 9px 9px 9px 9px;
}

.container{
  max-width: 1300px;
  margin-left: auto;
  margin-right: auto;
}


.image-container{
  display: flex;
  overflow: scroll;
}

.image-item{
  position: relative;
  min-width: 25%;
  box-sizing: border-box;
  left: 0;

  }

@media only screen and (min-width: 600px)  {

  .cards{
    align-items: stretch;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: flex-start;
  width:100%;
  }

  .container{
    display: flex;
  }

  .content-container{
    margin-top: 70%;
    
  }

  img{
        border-radius: 16px 16px 0px 0px;

  }

  .card{
        border-radius: 16px 16px 16px 16px;

  }

  .image-item{
  position: absolute;

  box-sizing: border-box;
  left: 0;
  
  }

  .card{

    width:100%;
    position: relative;
    -webkit-box-shadow: 0px 0px 18px -4px rgba(0,0,0,0.56);
-moz-box-shadow: 0px 0px 18px -4px rgba(0,0,0,0.56);
box-shadow: 0px 0px 18px -4px rgba(0,0,0,0.56);
  }

  .card-container{
    width: 30%;
  }


}
</style>
