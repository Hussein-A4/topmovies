<template>
<div>
  <select v-model="selected_movie">
    <!-- inline object literal -->
    <option v-for="movie in movies_list" :value="movie.id">{{movie.name}}</option>
  </select>
  <button @click="getOption()">test</button>
  <p>{{response_data.movie_title}}</p>
  <img :src=response_data.img alt="">
</div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      selected_movie: null,
      response_data:
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
        this.response_data.movie_title = movieData.data.original_title;
        this.response_data.release_date = movieData.data.release_date;
        this.response_data.popularity = movieData.data.popularity;
        this.response_data.vote_average = movieData.data.vote_average;
        this.response_data.vote_count = movieData.data.vote_count;
        this.response_data.language = movieData.data.language;
        this.response_data.budget = movieData.data.budget;
        this.response_data.overview = movieData.data.overview;

      })
// this.response_data to get info
    }
  }


</script>

<style>
</style>