<template>
  <div class="card">
    <div class="card-image">
      <figure class="image is-3by4">
        <img :src="film.Poster" alt="Placeholder image" />
      </figure>
    </div>
    <div class="card-content">
      <div class="media">
        <div class="media-content">
          <p class="title is-4">{{film.Title}}</p>
          <p class="subtitle is-6">Year {{film.Year}} - Genre {{film.Genre}}</p>
        </div>
      </div>

      <div v-if="show">{{film.Plot}}</div>

      <b-button @click="show = !show" rounded>Toggle Plot</b-button>
    </div>
  </div>
</template>


<script>
import axios from "axios";
export default {
  name: "FilmDetail",
  data() {
    return {
      film: {},
      show: false
    };
  },
  props: {
    imdbID: {
      type: String,
      required: true
    }
  },
  methods: {
    getFilmDetails() {
      let endpoint = `http://www.omdbapi.com/?i=${this.imdbID}&plot=full&apikey=20b32a5f`;
      axios.get(endpoint).then(resp => {
        this.film = resp.data;
      });
    }
  },
  created() {
    this.getFilmDetails();
  }
};
</script>