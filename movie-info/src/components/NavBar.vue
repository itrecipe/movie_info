<!-- 파일 생성 후 자동완성 기능 : vinit 입력 후 엔터를 치면 
         기본 코드 스니펫이 자동완성 된다.
-->
<template>
    <nav class="navbar">
        <a href="#">Home</a>
        <a href="#">Movies</a>
        <a href="#">About</a>
    </nav>
</template>

<script>
    export default { //모듈을 꺼내오기 위한 방법
        name: "NavBarComponent" //name부분 작성방법 -> name: 파일명+component 이런 형식으로 작성할것
    }
</script>

<style>
    .navbar {
        background-color: #000;
        padding: 20px;
        text-align: center; /* 가운데 정렬 */
    }

    .navbar a {
        color: #fff;
        text-decoration: none;
        padding: 1em; /* 여백 추가 */
    }
</style>
