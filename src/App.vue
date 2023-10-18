<script setup>
import { data } from "./cars.json";
import {ref} from "vue"
const cars = ref(data)
</script>

<template>
  <div class="container">
     <div class="sideBar">Sidebar placeholder</div>
     <div class="cars">
        <template  v-for="(question, index) in cars" :key="index">
           <template v-if="index == 4">
              <div class="car-container">
                 <div class="value-your-car card">
                    <p class="title">Value your car</p>
                    <p>Find out the value of your car in just a few minutes.</p>
                 </div>
              </div>
           </template>
           <div class="car-container">
              <article class="card"  >
                 <div class="image-container">
                    <div class="image-item" v-for="image in question.media_urls[0]" :key="image">
                       <img :src="image">
                       <div class="bottomTabs">
                          <p class="pill">{{Math.round(question.odometer_value/1000)}}k {{ question.odometer_units }}</p>
                       </div>
                    </div>
                 </div>
                 <div class="vehicle-information">
                    <div class="featured-information">
                       <p class="featured-pill">{{ question.advert_classification }}</p>
                    </div>
                    <div class="content">
                       <div>
                          <h3>{{ question.plate }} {{ question.make }}</h3>
                          <h4 class="sub-title">{{ question.derivative }}</h4>
                       </div>
                       <div class="content-bottom">
                          <div class="mobile-content">
                             <p>{{Math.round(question.odometer_value/1000)}}k {{ question.odometer_units }} <span class="separator">|</span> {{ question.fuel_type }}</p>
                             <p>{{question.transmission.charAt(0).toUpperCase() + question.transmission.slice(1).toLowerCase()}} <span class="separator">|</span> {{ question.body_type }}</p>
                          </div>
                          <div class="price-container">
                             <h5><b>£550.90</b><span> /mo (PCP)</span></h5>
                             <h5 class="financeTagline">£23,300<span> Calculate</span></h5>
                          </div>
                       </div>
                       <div class="cta-container">
                          <FontAwesomeIcon icon="fa-solid fa-star" />
                          <button class="viewButton">View</button>
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
$breakpoint-desktop: 1024px;
$breakpoint-tablet: 600px;

.value-your-car {
  display: none;
}

h4 {
  margin: 0px;
}

h3 {
  margin: 0px;
}

h1,
h2,
h3,
h4,
h5 {
  margin: 0rem;
  font-family: "Overpass", sans-serif;
  line-height: 1.3;
}

h1 {
  margin-top: 0;
  font-size: 1.383rem;
}

h2 {
  font-size: 1.296rem;
}

h3 {
  font-size: 1.215rem;
}

h4 {
  font-size: 1.138rem;
}

h5 {
  font-size: 1.067rem;
}

p {
  font-size: 1rem;
}

.image-container {
  overflow: visible;
}

.sub-title {
  color: rgb(85, 89, 93);
}

.separator {
  font-size: 10px;
}
.financeTagline {
  margin: 4px 0px;
}

.content-bottom {
  display: flex;
}

.mobile-content {
  display: flex;
  flex-grow: 1;
  flex-direction: column;
  color: rgb(85, 89, 93);
  p {
    margin: 0;
  }
}

.cta-container {
  display: none;
}
.card {
  position: relative;
  font-family: "Overpass", sans-serif;
}

.sideBar {
  display: none;
}

.car-container {
  margin: 0px 0px 20px 5px;
}

img {
  height: 100%;
  -o-object-fit: cover;
  object-fit: cover;
  width: 100%;
  border-radius: 9px 9px 9px 9px;
}

.container {
  max-width: 1950px;
  margin-left: auto;
  margin-right: auto;
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
  width: 103%;
  height: 70%;
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
    right: 0;
    font-size: 12px;
    line-height: 18px;
    background: #3f3a50;
    color: white;
    border-radius: 8px;
    z-index: 99;
    border: 1px solid rgba(255, 255, 255, 0.2);
    padding: 3px 10px 2px 10px;
  }
}

.vehicle-information {
  padding: 15px 0px;
}

.content {
  position: relative;
  display: flex;
  gap: 1rem;
  flex-direction: column;
  padding: 0.5rem;
}

@media (min-width: $breakpoint-tablet) {
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

    .featured-pill {
      position: relative;
      font-size: 16px;
      line-height: 27px;
    }
  }

  .bottomTabs {
    left: 10px;
    position: absolute;
    display: block;
    bottom: 0;
  }

  .mobile-content {
    display: none;
  }

  .viewButton {
    padding: 11px 25px 12px 25px;
    background-color: #7572ff;
    border-radius: 16px;
    color: white;
    border: 0;
    line-height: 27px;
  }

  .cta-container {
    position: absolute;
    bottom: 0;
    right: 0;
  }

  .car-container {
    margin: 0px 0px 0px 0px;
  }
  .image-container:after {
    content: none;
  }

  .cars {
    align-items: stretch;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: flex-start;
    width: 100%;
    justify-content: center;
  }

  .container {
    display: flex;
    padding: 0 2% 0 2%;
  }

  .vehicle-information {
    margin: 70% 0px 0px 0px;
    padding: 0% 3% 3%;
  }

  img {
    border-radius: 16px 16px 0px 0px;
  }

  .card {
    border-radius: 16px 16px 16px 16px;
  }

  .image-item {
    position: absolute;

    box-sizing: border-box;
    left: 0;
  }

  .car-container {
    width: 45%;
    padding: 1%;
    .card {
      width: 100%;
      position: relative;
      -webkit-box-shadow: 0px 0px 25px 0px rgba(0, 0, 0, 0.15);
      -moz-box-shadow: 0px 0px 25px 0px rgba(0, 0, 0, 0.15);
      box-shadow: 0px 0px 25px 0px rgba(0, 0, 0, 0.15);
      transition-duration: 0.1s;
      transition-property: box-shadow, transform;
      min-height: 100%;
    }
    .card:hover {
      -webkit-box-shadow: 0px 0px 25px 0px rgba(0, 0, 0, 0.3);
      -moz-box-shadow: 0px 0px 25px 0px rgba(0, 0, 0, 0.3);
      box-shadow: 0px 0px 25px 0px rgba(0, 0, 0, 0.3);
    }
  }
}

@media (min-width: $breakpoint-desktop) {
  .card:hover {
    cursor: pointer;
    .cta-container {
      display: block;
    }
  }
  .sideBar {
    width: 28%;
    display: block;
  }

  .car-container {
    width: 30%;
    padding: 1%;
    margin-right: auto;
  }
}




</style>
