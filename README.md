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

## * App.vue

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
