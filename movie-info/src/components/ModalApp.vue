<!-- 모달창 만들기 -->
<template>
 <div class="modal" v-if="isModal">
      <div class="inner">
        <h3>{{data[selectedMovie].title}}</h3> <!-- {{data[selectedMovie].title}}에 selectedMovie를 인덱스 번호로 넣어 참조 하도록 구현-->
        <p>영화 상세정보</p>
        <!-- <button @click="isModal=false">닫기</button> props를 쓰기전 컴포넌트 분리전에 작성한 버튼 이벤트 -->
        
        <!-- <button @click="$emit('closeModal')">닫기</button> 
         vue는 자식이 부모 컴포넌트에게 데이터 변경 요청을 할 수 있는데
         $emit 함수를 사용해서 커스텀 함수 'closeModal' 이라는 이벤트를 
         만들어 전달 해주면 된다. -->
         <button @click="$emit('closeModal')">닫기</button>
        
      </div>
</div>
</template>

<script>
export default {
    name: "ModalComponent",
    /* props는 자바에 parameter(매개변수)와 같은 개념이다.
      props로 전달받은 데이터는 부모만 변경이 가능하다.
    */
    props: { 
      data: Array,
      isModal: Boolean,
      selectedMovie: Number
    }
  }
</script>

<style></style>