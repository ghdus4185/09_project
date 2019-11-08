# project 09 - Vue

##  목표

- node 개발 환경과 webpack에 대한 이해
- 컴포넌트 기반의 구조에 대한 이해
- axios를 통한 비동기적 데이터 처리에 대한 이해
- Vue.js 개발 프로세스를 통한 영화 목록 페이지 구현



### 1. 컴포넌트 구조

![1573198279762](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1573198279762.png)

### 2. 컴포넌트별 구현 화면

##### 1. App.vue (부모 vue)

![1573198465010](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1573198465010.png)

#### 2. MovieList.vue

![1573198499281](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1573198499281.png)

#### 3. MovieListItem.vue

![1573198520975](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1573198520975.png)

#### 4. MovieListItemModal.vue

![1573198541211](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1573198541211.png)



###### - app.vue

`import MovieList from './components/movies/MovieList'` : 저장되어있는 자식 컴포넌트를 불러온다.

MovieList를 불러왔으니까 components에 등록한다.

data에 안에 활용할 데이터를 정의

mounted 함수에 movies_URL, genre_URL을 가지고와서 axios로 받아 원하는 data만 return에 선언한 변수에 저장한다.

저장된 변수를 <MovieList :자식에서 부를 이름="부모가 가지고 있는 데이터"/> MovieList로 보내준다.

###### - MovieList.vue

app.vue로 부터 받은 변수를 사용하기 위해서 props를 설정한다(type도 설정해줘야함)

넘겨줄 MovieListItem을 불러온다.` import MovieListItem from './MovieListItem'`

불러왔으니까 components에 등록한다.  components: {  MovieListItem }

MovieListItem을 for문 돌려서 카드형식으로 출력

`<MovieListItem v-for="movie in selectGenre" :key='movie.id' :movie="movie"/>`

여기서 한줄에 4개씩 보이개 하기 위해 `<div class="row"><div>`로 감싸준다.



드롭다운으로 필터링해서 같은 장르만 보기 위해 data에 활용할 데이터를 정의한다. selectedGenreId 선언

드롭다운 selectedGenreId data와 양방향바인딩(v-model)이 시켜준다. 

`<select class="form-control" v-model="selectedGenreId">`

value에는 movie.genre_id와 비교하기 위해서 보내줄 정보 genre.id를 보여주는곳에는 genre.name을 보여준다.

`<option v-for="genre in genreList" :key="genre.id" :value="genre.id">{{genre.name}}</option>`

computed에 selectGenre함수를 만들어서 dropbox에서

`selectGenre(){if (this.selectedGenreId === ""){return this.movieList}else{return this.movieList.filter(movie=>{return movie.genre_id === this.selectedGenreId})}}},`

###### - MovieListItem.vue

데이터를 받기 위해서 props를 설정

MovieListItemModal를 불러옴

components에 등록

props로 받은 movie로 세부내용 작성

###### - MovieListItemModal.vue

모달 연결을 위해서 data-target을 주소로 받아서 연결시켜준다.

`<div class="modal fade" tabindex="-1" role="dialog" :id="`movie-${movie.id}`">`

모달에서의 이미지 출력

`<img :src="movie.poster_url" :alt="movie.name" style="width: 18rem;">`





### 5. 어려웠던 점

- genre.json, movie.json을 url로 등록해서 사용하기
  - Github - New gist  - filename을 genre.json or movie.json으로 설정 - content에 genre.json 내용 저장 - create publick gist
- method, mounted, computed의 차이점

- `v-bind:src="movie.poster_url" :alt="movie.name"` 처럼 모든 것을 v-bind로 연결되어 사용
- `<button class="btn btn-primary" data-toggle="modal" :data-target="`#movie-${movie.id}`">영화 정보 상세보기</button>`모달으로 data-target을 보내줄 때 앞에 #을 붙여야하고 `` 로 변수표시해서 보내줘야한다.