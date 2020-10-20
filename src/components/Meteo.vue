<template>
  <div class="container">
    <h1 class="my-4">App météo avec Vue js</h1>
    <div class="form-groupe mb-5">
      <label for="position">Entrez le nom d'une ville</label>
      <input
        type="text"
        name="position"
        id="position"
        class="form-control"
        v-model="requete"
        v-on:keypress="goMeteo"
      />
    </div>
    <div class="w-75 m-auto" v-if="temps">
      <h3 class="text-center mb-3">Position : {{ temps.name }}</h3>
      <div class="card text-center p-5">
        <p class="texte-affichage">
          Temperature : {{ temps.main.temp.toFixed() }}°
        </p>
        <p class="texte-affichage">
          Temps : {{ temps.weather[0].description }}
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import Axios from "axios";
export default {
  name: "meteo",
  data() {
    return {
      requete: "",
      apiKey: "ff732c46178296c3b6cef2f37d988be3",
      temps: undefined,
      urlApi: "https://api.openweathermap.org/data/2.5/weather?",
    };
  },
  methods: {
    goMeteo(e) {
      if (e.key === "Enter") {
        // Axios.get(
        //   `https://api.openweathermap.org/data/2.5/weather?q=${this.requete}&appid=${this.apiKey}`
        // ).then((response) => console.log(response));

        // console.log(this.requete);

        Axios.get(
          `${this.urlApi}q=${this.requete}&appid=${this.apiKey}&lang=fr&units=metric`
        ).then((response) => {
          this.temps = response.data;
          //   console.log(this.temps);
        });

        this.requete = "";
      }
    },
  },
};
</script>

<style scoped>
.texte-affichage {
  font-size: 30px;
  font-weight: 300;
  line-height: 1.2;
}
</style>
