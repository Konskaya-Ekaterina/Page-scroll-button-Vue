<template>
  <!--  Для корректной работы кнопки в мобильной версии должны быть два блока, один - в самом верху, второй - в самом низу-->
  <!--  У обоих блоков должны быть установлены id, ссылки на которые будут в href мобильных кнопок-->
  <div id="top"></div>

  <div class="container">
    <h1>Очень длинный текст</h1>
    <HelloWorld/>
  </div>

  <page-scroll-button/>

  <!--  Нижний блок может быть самостоятельным или быть, например, частью футера-->
  <h3>Конец страницы</h3>
  <div id="bottom"></div>
</template>

<script>
import HelloWorld from '@/components/HelloWorld.vue'
import PageScrollButton from "@/components/PageScrollButton";

export default {
  name: 'App',
  components: {
    HelloWorld,
    PageScrollButton
  },
}
</script>

<style lang="scss">

$mobile-breakpoint: 768px;
$container-width: 1200px;

html, body {
  overflow-x: hidden;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  width: 100vw;
  height: 100%;
  min-height: 100%;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

#top, #bottom {
  width: 100vw;
  height: 0;
  z-index: -10;
}

h1 {
  margin-bottom: 25px;

  @media (max-width: $mobile-breakpoint) {
    font-size: 22px;
  }
}

h3 {
  text-align: center;
  @media (max-width: $mobile-breakpoint) {
    font-size: 18px;
  }
}

.container {
  max-width: $container-width;
  margin: 0 auto;
  padding: 60px 0 40px;

  @media (max-width: $mobile-breakpoint) {
    width: 100vw;
    min-width: 320px;
    max-width: 560px;
    padding: 30px 10px 20px;
  }
}

</style>