<template>
  <div id="app" :dark-mode="darkMode">
    <header>
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
  </div>
</template>

<style lang="scss">
$font: "Nunito Sans", sans-serif;
$light-color: #fff;
$dark-color: #2c3e50;

body {
  margin: 0;
}
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  font-family: $font;
  color: $dark-color;
}
#app[dark-mode="true"] {
  color: $light-color;
  background-color: $dark-color;
}

header {
  padding: 0 80px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  /* offset-x | offset-y | blur-radius | spread-radius | color */
  box-shadow: 0px 2px 4px 0px rgba(0, 0, 0, 0.056);
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
</style>
<script>
export default {
  data() {
    return {
      darkMode: false,
    };
  },
};
</script>
