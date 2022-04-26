<template>
  <div id="app" :dark-mode="darkMode">
    <header :dark-mode="darkMode">
      <h1>Where in the world</h1>
      <button class="btn" @click="darkMode = !darkMode">
        <div v-if="!darkMode">
          <font-awesome-icon icon="fa-regular fa-moon" />
          <span>Dark Mode</span>
        </div>
        <div v-else>
          <font-awesome-icon icon="fa-regular fa-sun" />
          <span>Light Mode</span>
        </div>
      </button>
    </header>
    <main>
      <section>
        <div class="searchbar">
          <font-awesome-icon icon="fa-solid fa-magnifying-glass" />
          <input type="text" placeholder="Search for a country..." />
        </div>
        <select name="region" id="region">
          <option value="filter">Filter by Region</option>
          <option value="africe">Africa</option>
          <option value="america">America</option>
          <option value="asia">Asia</option>
          <option value="europe">Europe</option>
          <option value="oceania">Cceania</option>
        </select>
      </section>
      <country-card
        :dark-mode="darkMode"
        :country-data="countryData"
      ></country-card>
    </main>
  </div>
</template>

<style lang="scss">
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

  // variables
  --font: "Nunito Sans", sans-serif;
  --background: #f2f2f2;
  --text: #111517;
  --secondary-background: #fff;
  --box-shadow: 0px 2px 4px 0px rgba(0, 0, 0, 0.056);
  --border-radius: 5px;
  --secondary-text: #848484;

  // init
  font-family: var(--font);
  color: var(--text);
  background-color: var(--background);
}
#app[dark-mode="true"] {
  --background: #202c36;
  --secondary-background: #2b3844;
  --text: #fff;
  --secondary-text: #fff;
}
body {
  margin: 0;
}

header {
  padding: 0 80px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  /* offset-x | offset-y | blur-radius | spread-radius | color */
  box-shadow: var(--box-shadow);
  background-color: var(--secondary-background);
}
header[dark-mode="true"] {
  background-color: var(--secondary-background);
}

button {
  height: 22px;
  background: none;
  border: none;
  cursor: pointer;
  font-family: inherit;
  font-weight: 600;
  font-size: 16px;
  color: inherit;
}

.svg-inline--fa {
  width: 20px;
  height: 20px;
  margin-right: 8px;
  transform: rotate(-20deg);
}
main {
  height: 100vh;
  margin: 80px 80px 0;
  display: flex;
  flex-direction: column;
}
section {
  display: flex;
  justify-content: space-between;
  margin-bottom: 48px;
}
.searchbar {
  display: flex;
  align-items: center;
  width: 480px-32px-32px;
  height: 56px-19px-19px;
  padding: 19px 32px;
  background-color: var(--secondary-background);
  box-shadow: var(--box-shadow);
  border-radius: var(--border-radius);
  color: var(--secondary-text);
}
.searchbar .svg-inline--fa {
  width: 18px;
  height: 18px;
  transform: rotate(0deg);
  color: inherit;
}
input {
  margin-left: 24px;
  border: none;
  outline: none;
  font-family: inherit;
  font-size: inherit;
  background-color: var(--secondary-background);
  color: inherit;
}
input::placeholder {
  color: inherit;
}
select {
  height: 56px;
  width: 200px-18px;
  border: none;
  padding: 18px;
  border-radius: var(--border-radius);
  box-shadow: var(--box-shadow);
  font-family: inherit;
  font-size: 14px;
  background-color: var(--secondary-background);
  color: inherit;
}
</style>
<script>
import axios from "axios";
import CountryCard from "@/components/CountryCard.vue";
export default {
  components: {
    CountryCard,
  },
  data() {
    return {
      darkMode: false,
      countryData: [],
    };
  },
  mounted() {
    axios
      .get("https://restcountries.com/v3.1/all")
      .then((response) => {
        this.countryData = response.data;
        console.log(this.countryData);
      })
      .catch(function (error) {
        // handle error
        console.log(error);
      })
      .then(function () {
        // always executed
      });
  },
};
</script>
