<template>
  <div id="app">
    <div class="container">
      <!-- 1-3. 호출하시오. 
        필요한 경우 props를 데이터를 보내줍니다.
      -->
      <!--<MovieList/: 자식에서 부를 이름="부모가 가지고 있는 데이터"> -->
      <MovieList :movieList="movies" :genreList="genres"/>
    </div>
  </div>
</template>

<script>

import axios from 'axios'
// 1-1. 저장되어 있는 MovieList 컴포넌트를 불러오고,
import MovieList from './components/movies/MovieList'

export default {
  name: 'app',
  // 1-2. 아래에 등록 후
  components: {
    MovieList,
  },
  data() {
    return {
      // 활용할 데이터를 정의하시오.
      movies: [],
      genres: []
    }
  },
  mounted() {
    // 0. mounted 되었을 때, 
    // 1) 제시된 URL로 요청을 통해 data의 movies 배열에 해당 하는 데이터를 넣으시오. 
    const Movies_URL = 'https://gist.githubusercontent.com/ghdus4185/44252f0a0c8d260baba518e5bde30343/raw/0f4b678da6461275a427f8ae377eaf8ee0185b87/movies.json'
    axios.get(Movies_URL)
      .then((response)=>{
        const movies = response.data
        this.movies = movies
        console.log(response.data)
      })
      .catch((error)=>{console.log(error)})
    // 2) 제시된 URL로 요청을 통해 data의 genres 배열에 해당 하는 데이터를 넣으시오.
    const Genre_URL = 'https://gist.githubusercontent.com/ghdus4185/2f3f45a399dea2c6bb47a0010c411c5d/raw/d1c2e9312d67acda518a40f123de680f27afd888/genre.json'
    axios.get(Genre_URL)
      .then((response)=>{
        const genres = response.data
        this.genres = genres
        console.log(response.data)
      })
      .catch((error)=>{
        console.log(error)
      })
    // axios는 위에 호출되어 있으며, node 설치도 완료되어 있습니다.

  },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
