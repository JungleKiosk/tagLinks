<script>
export default {
  name: 'LinksView',
  data() {
    return {
      links: []
    }
  },
  created() {
    fetch('/src/data/data.json')
      .then(response => response.json())
      .then(data => {
        this.links = data;
      })
      .catch(error => console.error('Errore nel caricamento dei dati:', error));
  }
}
</script>



<template>
    <div class="links-container">
        <div v-for="link in links" :key="link.id" class="card">
            <h3>{{ link.title }}</h3>
            <p>{{ link.description }}</p>
            <a :href="link.url" target="_blank">Visita</a>
        </div>
    </div>
</template>


<style scoped>
.links-container {
    display: flex;
    flex-wrap: wrap;
    gap: 16px;
}

.card {
    border: 1px solid #ddd;
    padding: 16px;
    border-radius: 8px;
    width: 200px;
}
</style>