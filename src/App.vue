<template>
  <div id="app">
    <div class="lang-select">
      <span class="lang" :class="{selected: lang === 'ENG'}" @click="setLang('ENG')">ENG</span> /
      <span class="lang" :class="{selected: lang === 'HAI'}" @click="setLang('HAI')">ՀԱՅ</span> /
      <span class="lang" :class="{selected: lang === 'RUS'}" @click="setLang('RUS')">РУС</span> 
    </div>
    <div class="scroll-hint" :style="{opacity}" @click="scrollToDescr">
      <img src = "arrow.svg" alt=""/>
    </div>
    <h1 class="header">{{getFromDict('title')}}</h1>
    <div class="container">
      <p>{{getFromDict('days')}}</p>
      <p>{{getFromDict('address')}}</p>
      <p>{{getFromDict('free')}}</p>
      <div style="position:relative;overflow:hidden;margin-top:20px">
        <a href="https://yandex.ru/maps/10262/yerevan/?utm_medium=mapframe&utm_source=maps" style="color:#eee;font-size:12px;position:absolute;top:0px;">
          Ереван
        </a>
        <a href="https://yandex.ru/maps/10262/yerevan/house/YE0Ycg9oSEYOQFpqfX14c3lqZw==/?ll=44.487960%2C40.192471&utm_medium=mapframe&utm_source=maps&z=17" style="color:#eee;font-size:12px;position:absolute;top:14px;">Улица Братьев Орбели, 63/1 — Яндекс Карты</a>
        <iframe src="https://yandex.ru/map-widget/v1/?ll=44.487960%2C40.192471&mode=whatshere&whatshere%5Bpoint%5D=44.487960%2C40.192471&whatshere%5Bzoom%5D=17&z=17" width="100%" height="400" frameborder="1" allowfullscreen="true" style="position:relative;"></iframe>
      </div>
      <br/>
      <br/>
      <p class="descr">{{getFromDict('p1')}}</p>
      <p class="descr">{{getFromDict('p2')}}</p>
      <p class="descr">{{getFromDict('p3')}}</p>
      <p class="descr">{{getFromDict('p4')}}</p>
    </div>
  </div>
</template>

<script>

const generateMultilang = (RUS, ENG, HAI ) => {
  return {RUS, ENG, HAI}
}

import {p1e, p1h, p1r, p2e, p2h, p2r, p3e, p3h, p3r, p4e, p4h, p4r} from './assets/description'

export default {
  name: 'App',
  components: {
  },
  data() {
    return {
      lang: 'ENG',
      windowTop: window.top.scrollY,
      dict: {
        title: generateMultilang('ТУПИК', 'DEADLOCK', 'ՓԱԿՈՒՂԻ'),
        days: generateMultilang('Чт, Пт, Сб, Вс — 18:00-22:00', 'Th, Fr, Sa, Su — 18:00-22:00', 'Հն Ու Շբ Կր — 18:00-22:00'),
        address: generateMultilang('улица Братьев Орбели, 63/1', '63/1 Orbeli Brothers St, Yerevan', '63/1 Օրբելի եղբայրների փողոց'),
        free: generateMultilang('Вход свободный', 'Free admission', 'Մուտք ազատ է'),
        p1: generateMultilang(p1r, p1e, p1h),
        p2: generateMultilang(p2r, p2e, p2h),
        p3: generateMultilang(p3r, p3e, p3h),
        p4: generateMultilang(p4r, p4e, p4h),
      }
    }
  },
  mounted() {
    window.addEventListener("scroll", this.onScroll)
  },
  beforeDestroy() {
    window.removeEventListener("scroll", this.onScroll)
  },
  computed: {
    opacity() {
      return Math.max((500 - this.windowTop)/500, 0)
    }
  },
   methods: {
    scrollToDescr() {
      window.scrollTo({
        top: 680,
        behavior: "smooth",
      });
    },
    onScroll() {
      this.windowTop = window.top.scrollY /* or: e.target.documentElement.scrollTop */
    },
    getFromDict(name) {
      return this.dict[name][this.lang]
    },
    setLang(lang) {
      this.lang = lang
    }
   }
}
</script>

<style>
* {
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #010101;
  padding: 20px 20px;
}

.lang-select {
  position: absolute;
  top: 10px;
  right: 20px;
}

.lang {
  color: rgb(112, 127, 140);
  cursor: pointer;
  font-weight: 600;
}

p {
  font-size: 18px;
  margin: 5px 0;
}

.selected {
  color: #010101;  
}

.container {
  max-width: 400px;
  margin: auto;
}

.scroll-hint {
  height: 50px;
  width: 50px;
  padding: 15px;
  border-radius: 25px;
  box-shadow:  0px 3px 8px 2px rgba(0, 0, 0, 0.377);
  position: fixed;
  right: 20px;
  bottom: 20px;
  z-index: 10;
  background-color: #fff;
}

img {
  width: 100%;
}

.header {
  margin-top: 50px;
  font-size: 70px;
  text-align: center;
}

.descr {
  text-align: justify;
  text-indent: 20px;
  margin: 10px 0;

}

@media only screen and (max-width: 400px) {
  .header {
    font-size: 45px;
  }
}

body {
  margin: 0;
}
</style>
