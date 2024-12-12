<template>
  <!-- <div class="event show"> 이전에는 이렇게 작성됬었음 -->

  <!-- 하지만 뷰에서는 v-bind 문법으로 상태값이 변경되어야 하기 때문에 
     <div class="event show" :class="{show : true}"> v-bind문법을
     사용해서 데이터 바인딩을 해줘야 한다. -->
    
    <div class="event" :class="{show : isOpen}">
    
    <p>{{ text }}</p>
    <!-- style을 동적으로 다루는 방법 
        (아래 x 버튼을 클릭하면 이벤트 창이 닫히도록 구현)
    -->
    <button @click="isOpen=false">X</button>
   </div>
</template>

<script>
export default {
    name: "EventComponent",
    props: {
      text: String,
      isEventOpen: Boolean,
    },
    data() { //이벤트창 활성화 & 비활성화에 따라 상태값이 바뀌어야 해서 데이터(상태값)를 추가했다.
      return {
        isOpen: true
      }
    }
}
</script>

<style>
    .event {
      background: #444;
      color: #fff;
      padding: 10px 20px;
      text-align: center;
      font-size: small;
      display: flex;
      justify-content: space-between;
      align-items: center;
      display: none;
    }

    .event p {
      margin: 0;
    }

    /* 조건부에 의해 보일지 말지 정할 옵션 */
    .show {
      display: flex;
    }
    
    .event button {
      margin: 0;
    }
</style>