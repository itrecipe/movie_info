<template>
  <NavBar /> 
  <EventBox :text="text[eventTextNum]"/>
    {{ eventTextNum }}
  <SearchBar :data="data_temp" @searchMovie="searchMovie($event)"/>
  <p>
    <button @click="showAllMovie">전체보기</button>
  </p>

  <MoviesList
  :data="data_temp"
  @openModal="isModal=true;selectedMovie=$event"
  @increseLike="increseLike($event)"/>  
  
  <ModalApp 
      :data="data"
      :isModal="isModal"
      :selectedMovie="selectedMovie"
      @closeModal="isModal=false"
  />
</template>

<script>
import data from './assets/movies';
import EventBox from './components/EventBox.vue';
import ModalApp from './components/ModalApp';
import MoviesList from './components/MoviesList.vue';
import NavBar from './components/NavBar';
import SearchBar from './components/SearchBar.vue';

console.log(data);
console.log(ModalApp);
console.log("MoviesList 값 : " + MoviesList);

  export default {
    name : 'App',
    data() {
      return { 
        isModal: false,
        data: data, // 원본 데이터
        data_temp: [...data], // 사본 데이터
        selectedMovie: 0,
        text : ['NEOPLIX - 연습용 영화 정보 표시 플랫폼',
                '디스니 100주년 기념작, 워시',
                '그날, 대한민국 운명이 뒤바뀌었다, 서울의 여름'
        ],
        eventTextNum: 0, // 배열 번호를 의미하는 변수, 위 3가지 텍스트가 일정 시간이 지나면 변환 되도록 구현하기 위해 만듬
        interval : null,
        // setInterval을 해제 시키려면 변수가 필요하여 생성함
      }
    },
    methods: { 

      /* 검색 기능 추가 하기 전 : 배열 인덱스로 모든 자료에 좋아요 카운트가 올라 갔었음
        increseLike(i) {
          this.data[i].like += 1; 
       },
      */

      increseLike(id) {
         // 일치하는 영화 자료의 id 값을 찾아 좋아요 카운트가 되게끔 수정
         this.data.find(movie => {
            if(movie.id == id) { // movie.id 값과 전달 받는 매개변수 id의 값이 일치하는지 확인
              movie.like += 1;
            }
         }) 
      },
      searchMovie(title) {
        // 영화 제목이 포함된 데이터를 가져오기
        this.data_temp = this.data.filter(movie => {
          return movie.title.includes(title); // 해당되는 영화 제목이 포함되어 있으면 해당 정보 리턴
        })
      },
      showAllMovie() {
        // 원본 데이터를 복사 해오기
        this.data_temp = [...this.data];
      }
    },
    components: { // 컴포넌트 등록 하는곳
      NavBar: NavBar,
      EventBox: EventBox,
      ModalApp: ModalApp,
      MoviesList: MoviesList,
      SearchBar: SearchBar,
    },
    mounted() {
      //이벤트 창에 일정시간이 경과하면 다른 광고 메시지가 노출 되도록 구현 해보기  
      console.log('mounted');

      /* 3초 후 딱 한번만 이벤트 광고 텍스트 변경 되는 로직
        setTimeout (() => {
          this.eventTextNum += 1;
        }, 3000)
      */

      // 3초마다 한번씩 0~2번의 텍스트 문구로 이벤트창 내용이 바뀌는 로직
      this.interval = setInterval(() => {
        if(this.eventTextNum == this.text.length - 1) {
          this.eventTextNum = 0;
        } else {
          this.eventTextNum += 1;
        }
      }, 3000)

      /* setInterval()를 쓰면서 문제점이 하나 있다면 한번 실행되면 계속 실행된다는 특성이 있어 
         컴포넌트가 종료되어도 계속 혼자 실행되고 있을 가능성이 있어 unmount (타이머를 강제로 해제) 
         시켜 줄 로직이 필요하다 
      */
    },
    unmounted() {
      clearInterval(this.interval); // 인터발을 해제
    }
  }
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