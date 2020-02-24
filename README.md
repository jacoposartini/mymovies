# mymovies (OMDb API Client)

The require for this project was to create a table of images of
some films thanks the OMDb API.


We created 3 files:

* Main.js – A file wrote in Javascript language that calls
the file App.vue.
* App.vue – The extension (.vue) stands for the name of
a framework of Javascript. And it prints the table of the
films with a little description of it, thanks to
FilmDetail.vue
* FilmDetail.vue – This file works with the App.vue
because it passes some parameters like the film title,
the year of release and the genre.

## App.vue

* At first we declared the library axios that makes the HTTP
requests and the component from file FilmDetail that
passes info of the film.

```javascript
import axios from "axios";
import FilmDetail from "./FilmDetail";
export default {
  name: "FilmList",
  components: {
    FilmDetail
  },
```

* In this part we declare an array (films:[]) that will contain
the name of the films. After that in the method getFilms()
we call a the file films.json which has only the name of the
films. After this, with a forEach we set an endpoint for the
films thanks to the standard link, but in the end of it we
set the name of the film, our API key and, if there are
some space between the name of the film, we put a “+”.

```javascript
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
```
* In the template the films array is printed through the v-for
function, which works like a forEach.

```javascript
    <div class="columns is-multiline">
      <div :key="film.imdbID" v-for="film in films" class="column is-half">
        <FilmDetail :imdbID="film.imdbID" />
      </div>
    </div>
```
## FilmDetail.vue

* At first we declared the library axios that makes the HTTP
requests and the component from file FilmDetail that
passes info of the film.

```javascript
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
```

* At the end of the code we declared the attributes that we
want to see and the film plot which is managed by a button.

```javascript
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
  ```





## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
