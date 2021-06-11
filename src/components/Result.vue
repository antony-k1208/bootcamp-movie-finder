<template>
  <div>
    <h2>Result</h2>

    <p>{{ title }}</p>

    <p>{{ year }}</p>

    <p>{{ actors }}</p>

    <p>{{ genre }}</p>

    <p>{{ production }}</p>

    <p>{{ director }}</p>

    <p>{{ country }}</p>

    <p>{{ awards }}</p>

    <p>{{ plot }}</p>
  </div>
  <button @click="goBack">Zurück zur Suche</button>
</template>

<script>
export default {
  name: "Result",
  props: {
    title: String,
    year: String,
    actors: String,
    genre: String,
    production: String,
    director: String,
    country: String,
    awards: String,
    plot: String,
  },
  methods: {
    goBack() {
      this.$emit("reset");
    },
  },
  emits: ["reset"],
};
</script>
