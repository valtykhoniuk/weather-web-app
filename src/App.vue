<script>
import axios from "axios";

export default {
  data() {
    return {
      city: "",
      error: "",
      info: null,
    };
  },

  computed: {
    cityName() {
      return "«" + this.city + "»";
    },
    showTemp() {
      return "Temperature: " + this.info.main.temp;
    },
    showFeelsLike() {
      return "Feels like: " + this.info.main.feels_like;
    },
    showMinTemp() {
      return "Minimal temperature: " + this.info.main.temp_min;
    },
    showMaxTemp() {
      return "Maximal temperature: " + this.info.main.temp_max;
    },
  },

  methods: {
    getWeather() {
      if (this.city.trim().length < 2) {
        this.error = "The name is too short";
        return false;
      }
      this.error = "";

      axios
        .get(
          `https://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=9aa75d5e7ba78ba2e3fa668d6e97cf82&units=metric`
        )
        .then((res) => {
          this.info = res.data;
        })
        .catch((err) => {
          this.error = "City not found";
          this.info = null;
        });
    },
  },
};
</script>

<!-- 21 line: @input="this.city = $event.target.value"
or
v-model="city" -->

<template>
  <div class="wrapper">
    <h1>Weather app</h1>
    <p>Get known weather in {{ city == "" ? "your city" : cityName }}</p>
    <input
      type="text"
      v-on:input="this.city = $event.target.value"
      placeholder="Write the name"
    />
    <button v-if="city != ''" v-on:click="getWeather()">Go!</button>
    <button disabled v-else>Enter name</button>
    <p class="error">{{ this.error }}</p>
    <div v-if="info != null">
      <p>{{ showTemp }}</p>
      <p>{{ showFeelsLike }}</p>
      <p>{{ showMinTemp }}</p>
      <p>{{ showMaxTemp }}</p>
    </div>
  </div>
</template>

<style scoped>
.error {
  color: red;
}

.wrapper {
  width: 900px;
  height: 500px;
  border-radius: 50px;
  padding: 20px;
  background-color: whitesmoke;
  text-align: center;
}

.wrapper h1 {
  margin-top: 50px;
}

.wrapper p {
  margin-top: 20px;
}

.wrapper input {
  margin-top: 30px;
  background: transparent;
  border: 0;
  border-bottom: 2px solid #ff9a3b;
  color: #ff9a3b;
  padding: 5px 8px;
  outline: none;
}

.wrapper input:focus {
  border-bottom: 2px solid #e77104;
}

.wrapper button {
  background: #ff9a3b;
  color: whitesmoke;
  border-radius: 10px;
  padding: 10px;
  border: none;
  margin-left: 20px;
  cursor: pointer;
  transition: transform 500ms ease;
}

.wrapper button:disabled {
  background-color: rgb(219, 219, 219);
}

.wrapper button:hover {
  transform: scale(1.1);
}
</style>
