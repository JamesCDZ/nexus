<script setup>
import { data } from "../cars.json";
import {ref} from "vue"
import slideControls from '../components/slideControls.vue'
import valueYourCar from '../components/valueYourCar.vue'
import favouriteIcon from '../components/favouriteIcon.vue'

// Import data from json
const cars = ref(data)

// Functions for card slideshows
function nextSlide(index){
  const scrollableElement = document.getElementById("scrollable-"+ index)
  const imageWidth = scrollableElement.clientWidth 
  scrollableElement.scrollLeft += imageWidth;
}

function previousSlide(index){
  const scrollableElement = document.getElementById("scrollable-"+ index)
  const imageWidth = scrollableElement.offsetWidth
  scrollableElement.scrollLeft -= imageWidth;
}

// Reset slideshows when page is resized
addEventListener("resize", (event) => {

  let slideShows = document.getElementsByClassName("image-container")
  for (const SlideShow of slideShows){
    SlideShow.scrollLeft=0
  }

});
</script>

<template>
  <div class="header">Header placeholder</div>
  <div class="container">
    <div class="sideBar">Sidebar placeholder</div>
    <div class="cars">
      <template v-for="(car, index) in cars" :key="index">
        <!-- Adds the "value your car" card as the 5th card -->
        <template v-if="index == 4">
          <div class="information-container">
            <valueYourCar />
          </div>
        </template>
        <!-- Car card template -->
        <div class="car-container">
          <article class="card">
            <!-- Image section -->
            <div class="image">
              <a :href="`#${car.make}`" :title="`View this ${car.advert_classification} ${car.plate } ${ car.make }. £550 per month`">
                <div class="image-container" :id="`scrollable-${index}`">
                  <template v-for="(image, id) in car.media_urls" :key="image">
                    <template v-if="id < 3">
                      <div class="image-item" :id="`${index}-${id}`">
                        <img :src="image.large" width="200" height="100" loading="eager">
                      </div>
                    </template>
                  </template>
                </div>
              </a>
              <!-- Imports the slideshow controls -->
              <slideControls @next-slide="nextSlide" @previous-slide="previousSlide" :id="index" />
            </div>
            <!-- Featured pill : Main pill displayed at the top left of cardon desktop -->
            <div class="vehicle-information">
              <div class="featured-information">
                <p class="featured-pill">{{ $filters.capitalise(car.advert_classification) }} </p>
              </div>
              <!-- Car information section -->
              <div class="content">
                <!-- Top half of the content box -->
                <div class="content-top">
                  <div class="car-details">
                    <h3>{{ car.plate }} {{ car.make }}</h3>
                    <h4 class="sub-title">{{ car.derivative }}</h4>
                  </div>
                  <!-- Importing the star icon -->
                  <div>
                    <favouriteIcon />
                  </div>
                </div>
                <!-- Bottom half of the content box -->
                <div class="content-bottom">
                  <div class="detail-pills">
                    <ul>
                      <li>{{Math.round(car.odometer_value/1000)}}k {{ car.odometer_units }}</li>
                      <li>{{ car.fuel_type }}</li>
                      <li>{{ $filters.capitalise(car.transmission) }}</li>
                      <li>{{ car.body_type }}</li>
                    </ul>
                  </div>
                  <div class="price-container">
                    <h2>£550.90 <span> /mo (PCP)</span>
                    </h2>
                    <h4 class="financeTagline">£23,300 <span> Calculate</span>
                    </h4>
                  </div>
                  <div class="cta-container">
                    <button class="viewButton">View</button>
                  </div>
                </div>
              </div>
            </div>
          </article>
        </div>
      </template>
    </div>
  </div>
</template>

<style scoped lang="scss">  
$breakpoint-desktop: 1500px;
$breakpoint-tablet: 600px;

ul {
  list-style: none;
  padding: 0;
  margin: 0px 10px 10px 0;
  li {
    float: left;
    padding: 2px 5px 2px 0px;
  }
  li + li:nth-child(even)::before {
    content: " | ";
  }
}

//Default mobile page styles
.header {
  display: none;
}

.image {
  position: relative;
}

.slide-controls {
  display: none;
}

h1,
h2,
h3,
h4,
h5 {
  margin: 0rem;
  font-family: "San Francisco";
  line-height: 1.3;
  font-weight: 400;
}

h1 {
  margin-top: 0;
  font-size: 1.383rem;
}

h2 {
  font-size: 1.067rem;
  font-weight: 700;

  span {
    font-weight: normal;
  }
}

h3 {
  font-size: 1.267rem;
  margin: 0;
  span {
    display: none;
  }
}

h4 {
  margin: 0;
}

p {
  font-size: 1rem;
}

.separator {
  font-size: 1rem;
}

.financeTagline {
  margin: 0.2rem 0;
}

.content-bottom,
.content-top {
  display: flex;
}

.car-details {
  display: flex;
  flex-direction: column;
  flex-grow: 1;
  .sub-title {
    color: rgb(85, 89, 93);
  }
}

.detail-pills {
  display: flex;
  flex-grow: 1;
  flex-direction: column;
  color: rgb(85, 89, 93);
  max-width: 50%;

  p {
    margin: 0;
  }
}

.cta-container {
  display: none;
}

.card {
  position: relative;
  font-family: "San Francisco";
}

.sideBar {
  display: none;
}

.car-container,
.information-container {
  margin: 0 0 0.1rem 0.3rem;
}

img {
  height: 100%;
  -o-object-fit: cover;
  object-fit: cover;
  width: 100%;
  border-radius: 9px;
}

.container {
  max-width: 1950px;
  margin-left: auto;
  margin-right: auto;
  overflow-x: hidden;
}

.image-container {
  display: flex;
  overflow-x: scroll;
  overflow-y: hidden;
  gap: 9px;
}

.image-container:after {
  content: "";
  position: absolute;
  z-index: 1;
  top: 0;
  left: 0;
  pointer-events: none;
  background-image: linear-gradient(
    to right,
    rgba(255, 255, 255, 0),
    rgb(255, 255, 255) 99rem
  );
  width: 100%;
  height: 100%;
}

.image-item {
  position: relative;
  min-width: 35%;
  box-sizing: border-box;
  left: 0;
}

.pill {
  background: #3f3a50;
  color: white;
  border-radius: 8px;
  z-index: 99;
  border: 1px solid rgba(255, 255, 255, 0.2);
  padding: 1px 10px 1px 10px;
}

.bottomTabs {
  display: none;
}

.featured-information {
  position: relative;
  top: 0;

  .featured-pill {
    position: absolute;
    font-size: 12px;
    line-height: 18px;
    background: #3f3a50;
    color: white;
    border-radius: 8px;
    z-index: 99;
    border: 1px solid rgba(255, 255, 255, 0.2);
    padding: 3px 10px 2px 10px;
    right: 3rem;
    margin-top: 0.6rem;
  }
}

.vehicle-information {
  padding: 8px 0px 0px 0px;
}

.content {
  position: relative;
  display: flex;
  gap: 0.5rem;
  flex-direction: column;
  padding: 10px 0px 10px 0px;
  margin: 0 0.8rem;
}

@media (min-width: $breakpoint-tablet) {
  ul {
    display: flex;
    gap: 2px;

    li {
      background: #3f3a50;
      border-radius: 8px;
      border: 1px solid rgba(255, 255, 255, 0.2);
      padding: 1px 5px 1px 5px;
      font-size: 15px;
    }
    li + li:nth-child(even)::before {
      content: "";
    }
  }

  h2 {
    font-size: 1.296rem;
  }

  h3 {
    span {
      display: block;
      white-space: pre-wrap;
      word-wrap: break-word;
      display: inline;
    }
  }

  .content {
    margin: 0;
    gap: 1rem;
  }

  .value-your-car {
    background: rgba(246, 247, 251, 1);
    border: 1px solid rgba(209, 214, 224, 1);
    display: block;
    text-align: center;

    .title {
      font-size: 32px;
    }
  }

  .featured-information {
    position: absolute;
    top: 0px;
    left: 10px;
    display: flex;

    .featured-pill {
      position: relative;
      font-size: 16px;
      line-height: 27px;
      right: 0rem;
      font-weight: 700;
    }
  }

  .bottomTabs {
    left: 10px;
    position: absolute;
    display: block;
    bottom: 0;
  }

  .detail-pills {
    display: block;
    top: -2.4rem;
    color: white;
    position: absolute;
    max-width: 100%;
  }

  .viewButton {
    background-color: #7572ff;
    border-radius: 16px;
    color: white;
    border: 0;
    line-height: 28px;
    font-family: "Overpass", sans-serif;
    height: 3rem;
    padding: 0px 0px 0px 0px;
    width: 6rem;
    margin: 0.9rem 0px;
    font-weight: 600;
    font-size: 16px;
  }

  .cta-container {
    position: absolute;
    bottom: 0;
    right: 0;
  }

  .image-container:after {
    content: none;
  }

  .image-container {
    position: relative;
    gap: 0px;
    overflow: hidden;
  }

  .cars {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    width: 100%;
    gap: 15px;
    justify-content: center;
  }

  .container {
    display: flex;
    padding: 0 2% 0 2%;
  }

  .vehicle-information {
    padding: 0% 3% 0%;
  }

  img {
    border-radius: 16px 16px 0px 0px;
  }

  .image-item {
    position: relative;
    box-sizing: border-box;
    left: 0;
    min-width: 100%;
  }

  .car-container,
  .information-container {
    width: 45%;
    margin: 0;
    .card {
      width: 100%;
      position: relative;
      -webkit-box-shadow: 0px 0px 25px 0px rgba(0, 0, 0, 0.15);
      -moz-box-shadow: 0px 0px 25px 0px rgba(0, 0, 0, 0.15);
      box-shadow: 0px 0px 25px 0px rgba(0, 0, 0, 0.15);
      transition-duration: 0.1s;
      transition-property: box-shadow, transform;
      min-height: 100%;
      border-radius: 16px 16px 16px 16px;
    }

    .card:hover {
      -webkit-box-shadow: 0px 0px 25px 0px rgba(0, 0, 0, 0.3);
      -moz-box-shadow: 0px 0px 25px 0px rgba(0, 0, 0, 0.3);
      box-shadow: 0px 0px 25px 0px rgba(0, 0, 0, 0.3);
    }
  }
}

@media (min-width: $breakpoint-desktop) {
  ul {
    gap: 5px;
    margin: 0px 10px 10px 0;
    li {
      border-radius: 8px;
      padding: 2px 10px;
      font-size: 15px;
    }
  }

  .header {
    min-height: 237px;
    display: block;
  }

  .image-container {
    gap: 0px;
  }

  .card:hover {
    cursor: pointer;

    .slide-controls {
      display: flex;
      position: absolute;
      color: white;
      right: 0;
      top: 0;
      margin: 16px;
    }

    .cta-container {
      display: block;
    }
  }

  .sideBar {
    width: 28%;
    display: block;
  }

  .car-container,
  .information-container {
    width: 32%;
    margin-right: 0;
    box-sizing: border-box;
  }

  .cars {
    justify-content: start;
  }
}
</style>
