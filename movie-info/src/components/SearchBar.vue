<template>
    <div class="search-box">
        <!-- 
            @input="inputText" 글 상자를 입력할 땐 인풋 이벤트가 필요하다.
            사용자의 입력 값을 받으려면 @input="inputText = $event.target.value"
            이렇게 작성해야 하고 js의 이벤트 리스너 문법과 같은 의미 
        -->

        <!-- <input type="search" 
              @input="inputText = $event.target.value" 
              placeholder="검색어를 입력 하세요!">  
        -->

        <!-- 위에 작성된 @input="inputText = $event.target.value" 코드를
             v-model="변수" 문법을 사용하여 축약형으로 작성할 수도 있다.
             v-model="변수"는 사용자에게 입력 받은 값을 변수에 알아서 저장한다.
        -->

        <!-- 여기서 사용된 v-model은 한글자씩 입력 될때마다
             너무 예민하게 반응하여 수시로 검사가 됨 (v-model의 특성이라고 함) 
            <input type="search" 
                v-model="inputText"
                placeholder="검색어를 입력 하세요!">  
        -->

        <!-- @change 이벤트 : 입력 후 엔터키를 치거나 확인 버튼을 누를 때 처리 된다. -->

        <!-- $event.target : 현재 입력 받고 있는 요소명
             $event.target.value : 현재 요소안에 입력 된 값
          -->
        <input 
            type="search" 
                @change="
                $emit('searchMovie', $event.target.value)
                inputText = $event.target.value;
                $event.target.value = '' // 사용자가 입력한 값을 다시 빈값으로 초기화
               "
               placeholder="검색어를 입력 하세요!">  
        <button>검색</button>
    </div>
    <p>{{ inputText }}</p>
</template>

<script>
export default {
    name: "SearchBarComponent",
    data() {
        return {
            inputText: '',
        }
    },
    props: {
        data: Array,
    },
    watch : { //watch는 특정 상태변수가 변경됨을 감지하는 hook, hook은 (가로챔을 의미한다.)
        //이 안에는 검사할 항목을 작성

        /*  검사할 변수명(변경값) { <- 검사할 변수명은 상태변수 값과 동일하게 작성하면 된다.
                로직
            }
        */
        inputText(name) {
            // 입력한 영화 제목이 데이터 안에 있는지 확인
            // if(name !== "노량") {
            //     alert('해당하는 영화가 없어요!');
            // }

            const findName = this.data.filter(movie => {
                // 객체 안의 data 라는 변수를 읽으려면 this 키워드로 참조해줘야 읽을 수 있다.

                return movie.title.includes(name);
                // includes(값) : 배열안에 특정 값이 있는지 알려준다.
            })
            console.log(findName);
            if(findName.length == 0) {
                alert("해당하는 자료가 없습니다!");
            }
        }
    }
}
</script>

<style>
    .search-box {
        padding: 10px;
        display: flex;
        justify-content: center;
    }

    .search-box input {
        padding: 5px 10px;
    }

    .search-box button {
        margin: 0;
    }
</style>