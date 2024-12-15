<template>
    <div id="map" style="width: 100%; height: 500px;"></div>
</template>

<script>
export default {
    name: "MapComponent",
    props: {
        theaters: Array, // 극장 정보를 전달 받는다.
    },
    data() {
        return {
            map: null, // 지도 객체
            markers: [], // 지도에 추가된 마커들
        };
    },
    watch: {
        theaters(newTheaters) {
            this.updateMapMarkers(newTheaters); // 극장 정보가 바뀌면 마커 업데이트
        }
    },
    mounted() {
        this.loadNaverMapApi()
            .then(() => {
                this.initMap(); // 지도 초기화
            })
            .catch((err) => {
                console.error("네이버 지도 API 로드 실패:", err);
            });
    },
    methods: {
        loadNaverMapApi() {
            return new Promise((resolve, reject) => {
                if (window.naver && window.naver.maps) {
                    resolve(); // 이미 로드된 경우
                    return;
                }
                const script = document.createElement("script");
                script.src = "https://openapi.map.naver.com/openapi/v3/maps.js?ncpClientId=니키여따느라";
                script.onload = resolve; // 로드 완료
                script.onerror = reject; // 로드 실패
                document.head.appendChild(script);
            });
        },
        initMap() {
      const mapOptions = {
        center: new naver.maps.LatLng(37.5665, 126.9780), // 초기 서울 중심 좌표
        zoom: 11,
      };

      this.map = new naver.maps.Map("map", mapOptions);
      this.updateMapMarkers(this.theaters); // 초기 극장 마커 표시
    },
    updateMapMarkers(theaters) {
      // 기존 마커 제거
      this.markers.forEach((marker) => {
        marker.setMap(null);
      });
      this.markers = [];

      // 새로운 마커 추가
      theaters.forEach((theater) => {
        const marker = new naver.maps.Marker({
          position: new naver.maps.LatLng(theater.latitude, theater.longitude),
          map: this.map,
        });

        const infoWindow = new naver.maps.InfoWindow({
          content: `<div style="padding:10px;">${theater.name}</div>`,
        });

        naver.maps.Event.addListener(marker, "click", () => {
          infoWindow.open(this.map, marker);
        });

        this.markers.push(marker); // 마커 목록에 추가
      });
    },
  },
};
</script>

<style>
#map {
    width: 100%; /* 원하는 너비 설정 */
    height: 500px; /* 원하는 높이 설정 */
    position: relative; /* 위치 설정 */
    z-index: 0; /* 지도 우선순위를 조정 */
  }
</style>