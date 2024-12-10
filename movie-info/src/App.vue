<template>

  <!-- 영화정보 표시해보기 (반복문 사용법과 데이터 바인딩 시키는 방법 학습) -->
  <h2>영화정보</h2>
  <div v-for="(movie, i) in data" :key="i">
    <!-- 변수 표시 하는 방법 (데이터 바인딩) --> 

    <!-- <p>장르 : {{ data[i].category }}</p> 길게 써서 데이터 바인딩을 통해 표현도 가능하지만 변수명(값)을 써서 바로 뽑는게 더 편함 -->

    <h3 class="bg-yellow" :style="textRed"> {{ movie.title }} </h3> <!-- :속성명="데이터" <- 속성에 값을 바인딩 할때 사용 (Vue 문법) -->
    <p>개봉 : {{ movie.year }}</p>
    <p>장르 : {{ movie.category }}</p>

    <!-- 배열 순서대로 값을 일일이 찍어 표현할때는 이렇게도 쓸 수 있음
    <p>{{ foods[0] }}</p>
    <p>{{ foods[1] }}</p>
    <p>{8{ foods[2] }}</p> -->
    
    <!-- 반복문 사용법 Vue 문법 -> v-for="(item, index) /* index는 배열번호를 의미 */ in 데이터" , :key="키값" <- 고유 번호를 인식할 수 있는 키값을 넣어줘야 함 -->
    <!-- <p v-for="(item, i) in foods" :key="i">{{ item }}</p> -->
    
    <!-- 버튼을 클릭 할때마다 좋아요 카운트 수가 올라가는 기능 만들어보기 -->
    <!--onClick 이벤트를 뷰에서 쓰는 방법 : v-on:이벤트명="실행코드" or 축약형으로도 적을수 있음 -> @:click="실행코드"-->    
    <button @:click="increseLike(i)">좋아요</button> <span>{{ movie.like }}</span>
    <!-- @:click="increseLike" 이 부분에 작성해야 될 코드가 길어지면 아래에 함수를 만들어 쓰면 된다. 
     그래서 생성한 함수가 increseLike 이다. 아래 methods 부분을 참고하자 -->
        
  </div>
</template>

<script>
  export default {
    name : 'App',
    data() { //data() {}는 상태변수를 저장하는 공간 (state value) : 화면에 자주 업데이트 되는 변수들을 정의한다.
      return { // return문은 필수로 들어가야하며, 값이 자주 바뀌어야 할때 사용 감쌀때는 꼭 중괄호로 감싸줘야함
        // foods: ["김밥", "순대", "만두"],
        
        // like : 0,

        data : [
          { 
            title: "노량",
            year: 2023,
            category: "액션, 드라마",
            textRed: "color: red",
            like: 0,
          },
          { 
            title: "아쿠아맨 & 로스트 킹덤",
            year: 2024,
            category: "액션, 드라마, 어드벤쳐",
            like: 0,
          },
          { 
            title: "7일의 휴가좀 주세요!",
            year: 2023,
            category: "판타지, 드라마",
            like: 0,
          },
        ]
      }
    },
    methods: { 
      // 개별적으로 좋아요 카운트 수가 올라가도록 작성한 코드
      increseLike(i) {
        this.data[i].like += 1; //객체 내부에서 사용하는 변수는 앞에 this를 붙여서 객체의 주소를 가르켜야(참조해야) 한다.
      }
      
      /* 개별적으로 좋아요 카운트가 되기 전에 작성된 코드
      increseLike() {
        this.like += 1; //객체 내부에서 사용하는 변수는 앞에 this를 붙여서 객체의 주소를 가르켜야(참조해야) 한다.
      }
      */
    }    
  }
</script>

<style>
  .bg-yellow {
    background-color: gold;
    padding: 10px;
  }
</style>