<template>
  <div id="app" :dark-mode="darkMode">
    <header :dark-mode="darkMode">
      <h1>Where in the world</h1>
      <button class="btn" @click="darkMode = !darkMode">
        <div v-if="darkMode == false">
          <font-awesome-icon icon="fa-regular fa-moon" />
          <span>Dark Mode</span>
        </div>
        <div v-if="darkMode == true">
          <font-awesome-icon v-if="darkMode == true" icon="fa-regular fa-sun" />
          <span>Light Mode</span>
        </div>
      </button>
    </header>
    <main><country-card :dark-mode="darkMode"></country-card></main>
  </div>
</template>

<style lang="scss">
$font: "Nunito Sans", sans-serif;
$light-background: #f2f2f2;
$white: #fff;
$light-text: #111517;
$dark-background: #202c36;
$dark-elements: #2b3844;

body {
  margin: 0;
}
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  font-family: $font;
  color: $dark-background;
  background-color: $light-background;
}
#app[dark-mode="true"] {
  color: $white;
  background-color: $dark-background;
}

header {
  padding: 0 80px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  /* offset-x | offset-y | blur-radius | spread-radius | color */
  box-shadow: 0px 2px 4px 0px rgba(0, 0, 0, 0.056);
  background-color: #fff;
}
header[dark-mode="true"] {
  background-color: $dark-elements;
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
  margin: 48px 80px;
}
</style>
<script>
import CountryCard from "@/components/CountryCard.vue";
export default {
  components: {
    CountryCard,
  },
  data() {
    return {
      darkMode: false,
    };
  },
};
</script>
