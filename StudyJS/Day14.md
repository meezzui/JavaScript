#### 웹접근성
+ 웹접근성이란??
  + 장애인, 고령자 등이 웹 사이트에서 제공하는 정보에 비장애인과 동등하게 접근하고 이해할 수 있도록 보장하는 것이다.
+ 기본적으로 지금 선택한 이미지가 어떤 이미지인지는 alt 값을 통해서 읽혀진다.
+ 그래서 alt값도 api연동을 해주어야 한다. 그래야 해당 이미지마다 그게 어떤 것을 가리키는 이미지인지를 알 수가 있다.
+ 예를들어, 현재 날씨 정보를 웹접근성에 맞게 정보를 알려주기 위해서는 날씨 정보와 같이 불러오는 이미지들의 alt값도 같이 연동을 해주어야 한다.

#### 현재 날씨에 맞는 alt 값 나타내기
+ 현재 날씨정보를 가져오는 것은 `openWeatherAPI`를 사용하였다.
+ `getOpenWeatherData()` 함수를 보면 `iconUrl`값과 `openWeatherAPIImgNameList`의 키값이 같으면 `this.weather.iconUrl = this.weatherImgs[weather]`이 로직을 탄다.
+ `this.weather.iconUrl = this.weatherImgs[weather]` : `weatherImgs`에 들어온 해당 키의 값을 `iconUrl`에 저장해준다.
+ `this.weather.alt = this.weatherAlt[weather]`
  + `[weather]`에 의미는 키값으로 해당 value 값을 찾는다는 것이다. 
  + 만약 weather자리에 sunny가 들어간다면 `weatherAlt`에 키값인 `sunny`에 `value`값을 `weather` 오브젝트 안에 선언해준 `alt`에 넣어준다.
  + 그러면 `weatherAlt`안에 해당 키값에 맞는 vaule값이 alt값에 넣어지게 된다.

+ `<img :src="weather.iconUrl" :alt="'현재날씨:' + weather.alt">` : 현재 날씨에 맞는 이미지와 alt값이 보여지게 된다.
![image](https://user-images.githubusercontent.com/86812098/174543003-b7746bbc-3209-4a2d-a4b5-7992f60ad017.png)

```node
<template>
<div v-if="weather.show" class="weather">
  <img :src="weather.iconUrl" :alt="'현재날씨:' + weather.alt">
  <div class="temp">{{weather.value}}</div>
</div>
</template>

<script>
  data(){
   weather: {
      show: false,
      iconUrl: '',
      value: '',
      alt: ''
    },
    openWeatherAPIImgNameList: {
      sunny: ['01d@2x', '01n@2x'],
      cloudy: ['02d@2x', '02n@2x', '03d@2x', '03n@2x', '04d@2x', '04n@2x', '50d@2x', '50n@2x'],
      rainy: ['09d@2x', '09n@2x', '10d@2x', '10n@2x', '11d@2x', '11n@2x'],
      snow: ['13d@2x', '13n@2x']
    },
    weatherImgs: {
      sunny: require('@/assets/image/weather-sunny.png'),
      cloudy: require('@/assets/image/weather-cloudy.png'),
      rainy: require('@/assets/image/weather-rainy.png'),
      snow: require('@/assets/image/weather-snow.png')
    },
    weatherAlt: {
      sunny: '맑음',
      cloudy: '흐림',
      rainy: '비',
      snow: '눈'
    }
  }
  
  methods: {
    getOpenWeatherData(lati, longi) {
      openWeatherData(lati, longi).then((res) => {
        this.weather.value = res.data.temp ? (res.data.temp.toFixed(0)) + '' : null
        for (const weather in this.openWeatherAPIImgNameList) {
          if (this.openWeatherAPIImgNameList[weather].find(o => res.data.iconUrl.includes(o))) {
            this.weather.iconUrl = this.weatherImgs[weather]
            this.weather.alt = this.weatherAlt[weather]
          }
        }
        this.$nextTick(() => {
          this.weather.show = !!this.weather.value
        })
      }).catch((e) => {
        console.log(e)
      }).finally(() => {
        //
      })
    }
  }
</script>

```
