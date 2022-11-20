<template>
<div>
  <select v-model="selected_movie">
    <!-- inline object literal -->
    <option v-for="movie in movies_list" :value="{number:movie.id}">{{movie.name}}</option>
  </select>
</div>
</template>

<script>
export default {
  data() {
    return {
      selected_movie: 557,
      movies_list: [
        {id:'557', name:'Spider-Man'},
        {id:'558', name:'Spider-Man2'},
        {id:'559', name:'Spider-Man'},
        {id:'2', name:'Spider-Man2'},
        {id:'557', name:'Spider-Man'},
        {id:'2', name:'Spider-Man2'},
        {id:'557', name:'Spider-Man'},
        {id:'2', name:'Spider-Man2'},
        {id:'557', name:'Spider-Man'},
        {id:'2', name:'Spider-Man2'}
      ]
    }
  }
}
</script>

<style>
</style>