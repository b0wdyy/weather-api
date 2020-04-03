<template>
  <div>
    Geef uw gemeente in: <input type="text" v-model="search_query" />
    <div v-if="weather">
      <p>{{ search_query }}</p>
      <h1>{{ weather.name }}</h1>
    </div>
    <div v-else>Loading...</div>
  </div>
</template>

<script>
export default {
  name: "Card",
  async mounted() {
    const url =
      "https://api.openweathermap.org/data/2.5/weather?q=Lommel&appid=fd2e801637d8bda81d0ec0252bb2cb09&units=metric";
    try {
      const res = await fetch(url);
      const data = await res.json();
      console.log(data);
      this.weather = data;
    } catch (error) {
      console.error(error);
    }
  },
  data() {
    return {
      weather: null,
      API_KEY: "fd2e801637d8bda81d0ec0252bb2cb09",
      FETCH_LINK: `https://api.openweathermap.org/data/2.5/weather?q=${this.search_query}&appid=${this.API_KEY}&units=metric`,
      search_query: ""
    };
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss"></style>
