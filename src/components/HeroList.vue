<template>
  <div class="page">
    <h1>Топ 10 героев Звездных войн</h1>
    <popup v-model="showPopup">
      <ol v-if="vehicles.length">
        <li v-for="(vehicle, i) in vehicles"
            :key="i"
        >
          Имя: {{vehicle.name}}, Модель: {{vehicle.model}},
          Производитель: {{vehicle.manufacturer}}, Длина: {{vehicle.length}},
          Максимальная скорость: {{vehicle.max_atmosphering_speed}},
          Экипаж: {{vehicle.crew}}, Пассажиры: {{vehicle.passengers}}
        </li>
      </ol>
      <div v-else>
        Нет машин
      </div>
    </popup>
    <ol class="list-hero">
      <li v-for="(hero, i) in heroes"
          :key="i"
          @click="getVehicles(hero.vehicles)"
          class="list-hero__item"
      >
        Имя: {{hero.name}}, Рост: {{hero.height}},
        Масса: {{hero.mass}}, Цвет волос: {{hero.hair_color}},
        Цвет кожи: {{hero.skin_color}}, Цвет глаз: {{hero.eye__color}},
        Год рождения: {{hero.birth_year}}, Пол: {{hero.gender}}
      </li>
    </ol>
  </div>
</template>

<script>
/* eslint-disable */
import axios from "axios";
import Popup from "./Popup";
export default {
  components: {
    Popup
  },
  data() {
    return {
      heroes: [],
      vehicles: [],
      showPopup: false
    }
  },
  methods: {
    getHeroes() {
      axios.get("https://swapi.dev/api/people/").then((result) => {
        this.heroes = result.data.results;
      })
    },
    getVehicles(vehicleUrls) {
      this.vehicles = [];
      this.showPopup = true;
      vehicleUrls.forEach((vehicleUrl) => {
        axios.get(vehicleUrl).then((result) => {
          this.vehicles.push(result.data);
        })
      })
    }
  },
  mounted() {
    this.getHeroes();
  }
}
</script>

<style>
.page {
  width: 900px;
  margin: 100px auto;
  background-color: #FEFEFE;
}
h1 {
  font-size: 30px;
  line-height: 30px;
  font-weight: 700;

}
.list-hero {
  margin-left: -40px;
  list-style: none;
  counter-reset: li;
}
.list-hero__item {
  position: relative;
  margin-bottom: 20px;
  border: 3px solid #2c6f9c;
  padding: 10px;
  border-radius: 4px;
  background: #FEFEFE;
  color: #231F20;
  font-size: 16px;
  line-height: 20px;
  cursor: pointer;
}
.list-hero__item:hover {
  box-shadow: 0 0 20px rgba(54, 77, 92, 0.3);
}
.list-hero__item:before {
  position: absolute;
  top: -12px;
  padding-left: 5px;
  padding-right: 5px;
  font-size: 16px;
  font-weight: bold;
  color: #2c6f9c;
  background: #FEFEFE;
  border-radius: 50%;
  counter-increment: li;
  content: counter(li);
}
@media screen and (max-width: 960px) {
  .page {
    margin: 0 auto;
    width: auto;
    padding: 0 10px;
  }
}
</style>