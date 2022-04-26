<template>
  <div id="component" :dark-mode="darkMode">
    <div class="flag"></div>
    <div class="country-info">
      <h1>Country</h1>
      <p>
        <span><b>Population:</b> Zahl</span>
        <span><b>Region:</b> Kontinent</span>
        <span><b>Capital:</b> Hauptstadt</span>
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "CountryCard",
  props: {
    darkMode: {
      type: Boolean,
      default: false,
    },
    countryData: {
      type: Array,
    },
  },
};
</script>

<style lang="scss" scoped>
#component {
  width: 264px;
  height: 336px;
  background-color: var(--secondary-background);
  color: var(--text);
  border-radius: var(--border-radius);
}
.flag {
  height: 40%;
  background-image: url("@/assets/logo.png");
}
.country-info {
  padding: 24px;
}
p {
  display: flex;
  flex-direction: column;
}
</style>
