<template>
  <header v-if="!hasSearchResult">
    <h1>Movie Finder</h1>
    <p>Search your movie</p>
    <input
      type="text"
      placeholder="Title"
      v-model="title"
      @keypress.enter="onClick"
    />
    <input
      type="text"
      placeholder="Year"
      v-model="year"
      @keypress.enter="onClick"
    />
    <button @click="onClick">Search</button>
  </header>
  <Result v-bind="resultNormalized" v-else @reset="onReset" />
  <!-- <Result
  :title="result.Title"
  :year="result.Year"
  :actors="result.Actors"
  :genre="result.Genre"
  :production="result.Production"
  :director="result.Director"
  :country="result.Country"
  :awards="result.Awards"
  :plot="result.Plot"
  @reset="onReset" /> -->
</template>

<script>
import Result from "./components/Result.vue";

export default {
  name: "App",
  components: {
    Result,
  },
  data() {
    return {
      title: "",
      year: "",
      result: {},
      hasSearchResult: false,
    };
  },
  computed: {
    resultNormalized() {
      let entries = Object.entries(this.result);
      entries = entries.map((entry) => {
        entry[0] = entry[0].toLowerCase();
        return entry;
      });
      return Object.fromEntries(entries);
    },
  },
  methods: {
    onClick() {
      if (this.title !== "") {
        fetch(
          "https://www.omdbapi.com/?apikey=167eb644&t=" +
            this.title +
            "&y=" +
            this.year
        )
          .then((response) => response.json())
          .then((data) => {
            this.result = data;
            this.hasSearchResult = true;
          });
      }
    },
    onReset() {
      this.result = {};
      this.hasSearchResult = false;
      this.title = "";
      this.year = "";
    },
  },
};
</script>

<style>
header {
  background-image: url("https://www.decopoint.at/media/image/product/94792/md/filmstreifen-kunststoff-140x19cm-art_nr7344641.jpg");
  background-size: cover;
  background-size: contain;
  background-repeat: no-repeat;
  background-position: 400px;
}
</style>
