<template>
  <div id="app">
    <div class="lang-select">
      <span class="lang" :class="{selected: lang === 'ENG'}" @click="setLang('ENG')">ENG</span> /
      <span class="lang" :class="{selected: lang === 'HAI'}" @click="setLang('HAI')">ՀԱՅ</span> /
      <span class="lang" :class="{selected: lang === 'RUS'}" @click="setLang('RUS')">РУС</span> 
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
        <iframe src="https://yandex.ru/map-widget/v1/?ll=44.487960%2C40.192471&mode=whatshere&whatshere%5Bpoint%5D=44.487960%2C40.192471&whatshere%5Bzoom%5D=17&z=17" width="100%" height="400" frameborder="1" allowfullscreen="true" style="position:relative;"></iframe></div>
    </div>
  </div>
</template>

<script>

const generateMultilang = (RUS, ENG, HAI ) => {
  return {RUS, ENG, HAI}
}

export default {
  name: 'App',
  components: {
  },
  data() {
    return {
      lang: 'ENG',
      dict: {
        title: generateMultilang('ТУПИК', 'DEADLOCK', 'ՓԱԿՈՒՂԻ'),
        days: generateMultilang('Чт, Пт, Сб, Вс — 16:00-22:00', 'Th, Fr, Sa, Su — 16:00-22:00', 'Հն Ու Շբ Կր — 16:00-22:00'),
        address: generateMultilang('улица Братьев Орбели, 63/1', '63/1 Orbeli Brothers St, Yerevan', '63/1 Օրբելի եղբայրների փողոց'),
        free: generateMultilang('Вход свободный', 'Free admission', 'Մուտք ազատ է'),
      }
    }
  },
   methods: {
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

.header {
  margin-top: 50px;
  font-size: 70px;
  text-align: center;
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
