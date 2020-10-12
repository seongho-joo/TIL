# 두 좌표사이의 거리 구하기

npm 모듈 중 `geolib` 설치

    $ npm i geolib

아래 코드처럼 `geolib.getDistance()` 활용  
함수 매개변수는 `obj`의 `value`는 <strong> latitude, longitude</strong> 로 선언해야한다.

    const geolib = require('geolib')

    const cur = {
      latitude: 35.113146371452984,
      longitude: 128.96482264377647,
    }
    const spot = {
      latitude: 35.11314232325089,
      longitude: 128.96483189063358,
    }

    console.log(geolib.getDistance(cur, spot) + ' meters')
