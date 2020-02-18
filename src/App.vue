<template>
  <div class="container" id="app">
    <!-- Main container -->

    <section class="hero">
      <div class="hero-body">
        <div class="container">
          <h1 class="title">
            MyMovies
            <img
              height="100"
              width="100"
              src="https://campbellpta.com/files/2018/09/popcorn-768x768.png"
            />
          </h1>
        </div>
      </div>
    </section>

    <div class="columns is-multiline">
      <div :key="film.imdbID" v-for="film in films" class="column is-half">
        <FilmDetail :imdbID="film.imdbID" />
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
import FilmDetail from "./FilmDetail";
export default {
  name: "FilmList",
  components: {
    FilmDetail
  },

  data() {
    return {
      films: []
    };
  },
  methods: {
    getFilms() {
      var filmTitles = require("./assets/films.json"); //["matrix", "star wars", "rambo", "django"]

      filmTitles.forEach(filmTitle => {
        let endpoint = `http://www.omdbapi.com/?s=${filmTitle.replace(
          " ",
          "+"
        )}&apikey=20b32a5f`;
        axios.get(endpoint).then(resp => {
          this.films = this.films.concat(resp.data.Search);
        });
      });
    }
  },
  created() {
    this.getFilms();
    document.title = "MyMovies";
  }
};
</script>