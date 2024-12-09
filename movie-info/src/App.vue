<template>
  <h2>영화정보</h2>
  <div>
    <!-- 변수 표시 하는 방법 (데이터 바인딩) --> 
    <h3 class="bg-yellow" :style="textRed"> {{ data[0].title }} </h3> <!-- :속성명="데이터" <- 속성에 값을 바인딩 할때 사용 (Vue 문법) -->
    <p>개봉 : {{ data[0].year }}</p>
    <p>장르 : {{ data[0].category }}</p>
    
    <!-- <p>{{ foods[0] }}</p>
    <p>{{ foods[1] }}</p>
    <p>{{ foods[2] }}</p> -->

    <!-- 반복문 사용법 Vue 문법 -> v-for="(item, index) /* index는 배열번호를 의미 */ in 데이터" , :key="키값" <- 고유 번호를 인식할 수 있는 키값을 넣어줘야 함 -->
    <p v-for="(item, i) in foods" :key="i">{{ item }}</p>
  </div>
</template>

<script>
  export default {
    name : 'App',
    data() { //상태변수(state value) : 화면에 자주 업데이트 되는 변수들을 정의함
      return { // return문은 필수로 들어가야하며, 값이 자주 바뀌어야 할때 사용 감쌀때는 꼭 중괄호로 감싸줘야함
        foods: ["김밥", "순대", "만두"],
        data : [
          { 
            title: "노량",
            year: 2023,
            category: "액션, 드라마",
            textRed: "color: red"
          },
          { 
            title: "아쿠아맨 & 로스트 킹덤",
            year: 2023,
            category: "액션, 드라마, 어드벤쳐",
          },
        ]
      }
    }    
  }
</script>

<style>
  .bg-yellow {
    background-color: gold;
    padding: 10px;
  }
</style>
