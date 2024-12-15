<!-- 영화 정보 리스트를 출력할 컴포넌트 -->
<template>
    <div class="container">
      <h2>영화정보</h2>
       <!-- <div v-for="(movie, i) in data" :key="i" class="item"> 
            영화 데이터를 검색시 배열 i값으로만 찾았더니 복사본 data_temp 기준에서  
            검색하여 데이터를 표시할때 기준이 달라져 버리는 문제가 발생함 그래서 이를 방지하기 위해
            밑에 key값에 고유한 id 값을 줘서 해당하는 자료를 찾을 수 있도록 변경 하였다.
            
            (검색시 고유한 id 값을 주기 전)
        -->
       <div v-for="(movie) in data" :key="movie.id" class="item" @click="$emit('showTheaters', movie.id)">
         <figure>
            <img :src="`${movie.imgUrl}`" :alt="movie.title">
          </figure>
          
          <div class="info">
            <h3 class="bg-yellow"> {{ movie.title }} </h3>
            <p>개봉 : {{ movie.year }}</p>
            <p>장르 : {{ movie.category }}</p>
                <!-- <button @:click="$emit('increseLike', i)">좋아요 
                    검색시 고유한 id값 주기 전-->

                <button @:click="$emit('increseLike', movie.id)">좋아요
                </button> 
                <span>{{ movie.like }}</span>
            <p>
                <!-- <button @click="$emit('openModal', i)">상세보기</button> 
                 여기도 역시 위와 같이 검색시 고유한 id값을 주기 전 -->

                <button @click="$emit('openModal', movie.id)">상세보기</button>
            </p>

            <p>
                <button @click="$emit('showTheaters', movie.id)">영화관 찾기</button> <!-- 이벤트 전달하기 -->
            </p>
      </div>
    </div>
</div>
</template>

<script>
export default {
    name: "MoviesListComponent", //컴포넌트명 등록하기
    
    // data: Array,
    props: ['data'],
}
</script>

<style>
    .container {
        padding: 20px;
    }
</style>