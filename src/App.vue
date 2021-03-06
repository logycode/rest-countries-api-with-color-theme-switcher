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
          <input
            type="text"
            v-model="searchString"
            placeholder="Search for a country..."
          />
        </div>
        <select name="region" id="region" v-model="selectedRegion">
          <option value="">Filter by Region</option>
          <option value="Africa">Africa</option>
          <option value="Americas">America</option>
          <option value="Asia">Asia</option>
          <option value="Europe" selected>Europe</option>
          <option value="Oceania">Cceania</option>
        </select>
      </section>
      <div class="row">
        <div id="component" v-for="(c, index) in showCountries" :key="index">
          <div class="flag">
            <img :src="c.flags.png" :alt="`${c.name.common} flag`" />
          </div>
          <div class="country-info">
            <h1>{{ c.name.common }}</h1>
            <p>
              <span><b>Population:</b> {{ population(c.population) }} </span>
              <span><b>Region:</b> {{ c.region }} </span>
              <span v-if="c.capital"
                ><b>Capital: </b>
                <a
                  :href="`https://www.google.com/maps/place/${c.name.common}`"
                  target="new"
                  >{{ c.capital[0] }}</a
                >
              </span>
            </p>
          </div>
        </div>
      </div>
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
  --link-color: #3686c9;

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
  --link-color: #369dc9;
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
  min-height: 100vh;
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
#component {
  width: 264px;
  // height: 336px;
  background-color: var(--secondary-background);
  color: var(--text);
  border-radius: var(--border-radius);
  margin-bottom: 2.5%;
  box-shadow: var(--box-shadow);
  overflow: hidden;
}
.row {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  margin: 0 -1%;

  // 1. you can use grid
  // 2. you can set a negative margin for the parent element

  > * {
    flex: 0 0 23%;
    margin: 0 1%;
  }
}
.flag {
  img {
    width: 100%;
    height: 200px;
    display: block;
  }
}
.country-info {
  padding: 24px;
}
p {
  display: flex;
  flex-direction: column;
}
a,
a:visited,
a:active {
  color: var(--link-color);
  font-weight: bold;
}
a:hover {
  text-decoration: none;
}
</style>
<script>
import axios from "axios";
export default {
  name: "App",
  data() {
    return {
      darkMode: false,
      countryData: [],
      selectedRegion: "",
      searchString: "",
    };
  },
  computed: {
    // Use computed properties once you need to return a value
    // filteredCountries() {
    //   if (this.selectedRegion === "" && this.countryEntered === "") {
    //     return this.countryData;
    //   } else if (this.selectedRegion !== "") {
    //     return this.countryData.filter(
    //       (item) =>
    //         item.region === this.selectedRegion &&
    //         item.name.common === this.countryEntered
    //     );
    //   } else {
    //     return this.countryData;
    //   }
    // },
    showCountries() {
      /*   if (this.selectedRegion === "") {
        this.countryData;
      }
      return this.countryEntered !== ""
        ? this.filteredCountriesBySearch
        : this.filteredCountriesByRegion;
    },
    filteredCountriesByRegion() {
      return this.countryData.filter(
        (item) => item.region === this.selectedRegion
      );
    },
    filteredCountriesBySearch() {
      return this.countryData.filter(
        (item) => item.region === this.selectedRegion
      ); */
      if (this.selectedRegion !== "") {
        if (this.searchString !== "") {
          return this.countryData.filter(
            (item) =>
              item.region === this.selectedRegion &&
              item.name.common === this.searchString
          );
        }
        return this.countryData.filter(
          (item) => item.region === this.selectedRegion
        );
      } else {
        return this.countryData;
      }
    },
  },
  methods: {
    // computed properties dont work with parameters I assume
    population(number) {
      return number.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
    },
  },
  mounted() {
    axios
      .get("https://restcountries.com/v3.1/all")
      .then((response) => {
        this.countryData = response.data;
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
