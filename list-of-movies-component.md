# List of Movies Component

Recall that you need a component that lists all the available movies, that is, those that are in the database. Your users can then pick from that list a movie to watch.

Add a `VideoList` component with the following content:

```markup
<template>
  <div>
    <div class="columns" v-for="i in Math.ceil(movies.length / 6)" :key="i">
      <div v-if="movies.length < 1">Loading...</div>
      <div v-else v-for="movie in movies.slice((i - 1) * 6, i * 6)" :key="movie._id" class="column">
        <img :src="cloudinaryInstance.url(movie.banner)" alt="" class="banner" @click="$emit('choose-movie', movie)">
      </div>
    </div>
  </div>
</template>
<script>
import axios from 'axios';
export default {
  props: ['cloudinaryInstance', 'movies'],
}
</script>
<style>
.banner {
  max-width: 204px;
  height: auto;
}
.banner:hover {
  cursor: pointer;
}
</style>
```

The properties that are passed are `cloudinaryInstance` and `movies`. The instance that resolves an image URL from its public ID while the `movies` array is being iterated shows a list of movies in a six-column grid.

Take a close look at the `img` tag:

```markup
<img :src="cloudinaryInstance.url(movie.banner)" alt="" class="banner" @click="$emit('choose-movie', movie)">
```

A `click` event is attached to each image. Clicking an image triggers an event called `choose-movie` to the parent component with a payload of the selected movie.

