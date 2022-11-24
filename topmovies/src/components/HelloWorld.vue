<template>
<div>
  <div>
    <select class="dropdown" v-model="selected_movie">
      <!-- inline object literal -->
      <option v-for="movie in movies_list" :value="movie.id">{{movie.name}}</option>
    </select>
  </div>
  <button id="getinfo" @click="getOption()">GET</button>
  <p>{{response_data.movie_title}}</p>
  <p> Release Date: {{response_data.release_date}} | Popularity: {{response_data.popularity}}</p>
  <p> Average Rating: {{response_data.vote_average}} | Vote Count: {{response_data.vote_count}}</p>
  <p> Language: {{response_data.original_language}} | Budget: ${{response_data.budget}}</p>
  <p> Overview: {{response_data.overview}}</p>
  <img :src=response_data.img alt="">
  <iframe :src=response_data.trailer frameborder="0" class="movieFrame"></iframe>
</div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      selected_movie: null,
      response_data:{
        movie_title:'',
        release_date:'',
        popularity:'',
        vote_average:'',
        vote_count:'',
        language:'',
        budget:'',
        overview:'',
        img: '',
        trailer: ''
      },
      movies_list: [
        {id:'557', name:'Spider-Man'},
        {id:'558', name:'Spider-Man 2'},
        {id:'559', name:'Spider-Man 3'},
        {id:'1930', name:'The Amazing Spider-Man'},
        {id:'102382', name:'The Amazing Spider-Man 2'},
        {id:'315635', name:'Spider-Man: Homecoming'},
        {id:'429617', name:'Spider-Man: Far from Home'},
        {id:'634649', name:'Spider-Man: No way home'},
        {id:'324857', name:'Spider-Man: Into the Spider-verse'},
        {id:'50410', name:'Spider-Man: The Venom Saga'}
      ]
    }
  },
  methods: {
    getOption() {
      axios.get(`https://api.themoviedb.org/3/movie/${this.selected_movie}`, {
      params: {
        api_key: "45f0db8e20f87e3e431aa1750076bb74",
        append_to_response: "videos",
      }
      }).then((movieData) => {
        console.log(movieData);
        let data =movieData.data
        const trailers = data.videos.results.filter((trailer) => trailer.type === "Trailer");
        this.response_data.movie_title = data.original_title;
        this.response_data.release_date = data.release_date;
        this.response_data.popularity = data.popularity;
        this.response_data.vote_average = data.vote_average;
        this.response_data.vote_count = data.vote_count;
        this.response_data.language = data.original_language;
        this.response_data.budget = data.budget;
        this.response_data.overview = data.overview;
        this.response_data.img = `https://image.tmdb.org/t/p/w500${data.poster_path}`;
        this.response_data.trailer = `https://www.youtube.com/embed/${trailers.at(0).key}`
      })
    }
  }
}
</script>

<style scoped>

img {
  flex: auto;
    width: 30vw;
    aspect-ratio: 2 / 3;
    border: 5px;
}

p {
  color: blue;
  font-weight: bold;
  font-family: Arial, Helvetica, sans-serif;
  text-align: center;
  width: 500px;
  margin: auto;
}

iframe {
  object-fit: contain;
  width: 60vw;
  aspect-ratio: 16 / 9;
  margin-left: auto;
  margin-right: auto;
  margin-top: auto;
  margin-bottom: auto;
  border: 3px solid blue;
}

body {
  background-color: rgb(255, 68, 68);
}

content{
  text-align: center;
}

.dropdown {
  position: flex;
  display: inline-block;
  background-color: rgb(255, 0, 0);
  color: white;
}

.dropdown a:hover {
  background-color: rgb(255, 118, 118);
}

#getinfo{
    background-color: #52fafa;
    color: rgb(255, 0, 0);
    padding: 15px 32px;
    text-align: center;
    text-decoration: none;
    font-size: 16px;
    cursor: pointer;
    font-weight: bold;
  }


</style>