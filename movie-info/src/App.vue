<template>
  <NavBar />
  <EventBox :text="text[eventTextNum]" />
  {{ eventTextNum }}
  <SearchBar :data="data_temp" @searchMovie="searchMovie($event)" />
  <p>
    <button @click="showAllMovie">전체보기</button>
  </p>

  <MoviesList
    :data="data_temp"
    @openModal="isModal=true;selectedMovie=$event"
    @increseLike="increseLike($event)"
    @showTheaters="showTheaters($event)"
  />

  <ModalApp
    :data="data"
    :isModal="isModal"
    :selectedMovie="selectedMovie"
    @closeModal="isModal=false"
  />

  <!-- MapComponent 추가 -->

  <!-- <MapComponent :latitude="37.5665" :longitude="126.9780" /> -->
  <MapComponent :theaters="selectedTheaters" /> <!-- 지도 컴포넌트에 극장 정보를 전달 한다.-->
</template>

<script>
import data from './assets/movies';
import EventBox from './components/EventBox.vue';
import ModalApp from './components/ModalApp';
import MoviesList from './components/MoviesList.vue';
import NavBar from './components/NavBar';
import SearchBar from './components/SearchBar.vue';
import MapComponent from './components/MapComponent.vue';

export default {
  name: 'App',
  components: {
    NavBar,
    EventBox,
    ModalApp,
    MoviesList,
    SearchBar,
    MapComponent, // 컴포넌트 등록
  },
  data() {
    return {
      isModal: false,
      data: data,
      data_temp: [...data], // 복사된 영화 데이터
      selectedMovie: [], // 선택된 영화의 극장 정보를 저장
      selectedTheaters: [], // 선택된 극장 정보 배열
      text: [
        'NEOPLIX - 연습용 영화 정보 표시 플랫폼',
        '디스니 100주년 기념작, 워시',
        '그날, 대한민국 운명이 뒤바뀌었다, 서울의 여름',
      ],
      eventTextNum: 0,
      interval: null,
    };
  },
  methods: {
    increseLike(id) {
      this.data.find((movie) => {
        if (movie.id == id) {
          movie.like += 1;
        }
      });
    },
    searchMovie(title) {
      this.data_temp = this.data.filter((movie) => {
        return movie.title.includes(title);
      });
    },
    showAllMovie() {
      this.data_temp = [...this.data];
    },
    showTheaters(id) {
      console.log("showTheaters id값이 제대로 전달 되는지 확인 : ", id);

      // 영화 id를 기반으로 극장 정보를 선택한다.
      const movie = this.data.find((movie) => movie.id == id);
        if (movie) {
          console.log("Selected movie theaters:", movie.theaters); 

          this.selectedTheaters = movie.theaters; // 극장 정보를 확인한다.
        }
    }
  },
  mounted() {
    this.interval = setInterval(() => {
      if (this.eventTextNum == this.text.length - 1) {
        this.eventTextNum = 0;
      } else {
        this.eventTextNum += 1;
      }
    }, 3000);
  },
  unmounted() {
    clearInterval(this.interval);
  },
};
</script>

<style>
  * {
    box-sizing: border-box;
    margin: 0;
  }

  body {
    max-width: 768px;
    margin: 0 auto;
    padding: 20px;
  }

  h1, h2, h3 {
    margin-bottom: 1rem;
  }

  p {
    margin-bottom: 0.5rem;
  }

  button {
    margin-right: 10px;
    margin-top: 1rem;
  }

  .item {
    width: 100%;
    border: 1px solid #ccc;
    display: flex;
    margin-bottom: 20px;
    padding: 1rem;
  }

  .item figure {
    width: 30%;
    margin-right: 1rem;
  }

  .item img {
    width: 100%;
  }

  .item .info {
    width: 100%;
  }

  .modal {
    background: rgba(0, 0, 0, 0.7);
    position: fixed;
    left: 0;
    top: 0;
    width: 100%;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .modal .inner {
    background: #fff;
    width: 80%;
    padding: 20px;
    border-radius: 10px;
  }
</style>
