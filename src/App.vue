<script>
import LinksView from './views/LinksView.vue'; // Importa il componente che gestisce i link

export default {
  components: {
    LinksView
  },
  data() {
    return {
      totalLinks: 0,
    };
  },
  created() {
    fetch('/src/data/data.json')
      .then(response => response.json())
      .then(data => {
        this.totalLinks = data.length;
      })
      .catch(error => console.error('Errore nel caricamento dei dati:', error));
  }
}
</script>

<template>
  <div id="header" class="container-fluid p-4 d-flex justify-content-between align-items-center">
    <div class="d-flex align-items-center">
      <h3 class="btn jk">
        <a href="https://github.com/JungleKiosk" target="_blank">JK</a>
      </h3>
    </div>
    <!-- <div class="word-slider">
      <h1 class="scrolling-text">
        🌴🐢🌴
      </h1>
      <h1 class="scrolling-text">
        🏖️🦆🌴
      </h1>
      <h1 class="scrolling-text">
        🌊🐬🌊
      </h1>
      <h1 class="scrolling-text">
        🌳🐿️🌳
      </h1>
      <h1 class="scrolling-text">
        🍂🦊🍂
      </h1>
      <h1 class="scrolling-text">
        🌙🌲🦉
      </h1>
    </div> -->
    <div>
      <span class="badge badge_bg ms-auto">Links: {{ totalLinks }}</span>
    </div>
  </div>
  <RouterView />
</template>

<style scoped></style>
