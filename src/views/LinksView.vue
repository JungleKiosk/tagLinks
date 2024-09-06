<script>
export default {
  name: 'LinksView',
  data() {
    return {
      searchQuery: '', // Variabile per memorizzare la parola chiave
      links: [],       // Array originale dei link
      filteredLinks: [] // Array dei link filtrati
    };
  },
  created() {
    // Carica i dati dal file JSON quando il componente è creato
    fetch('/src/data/data.json')
      .then(response => response.json())
      .then(data => {
        this.links = data;
        this.filteredLinks = data; // Inizializza i link filtrati con tutti i dati
      })
      .catch(error => console.error('Errore nel caricamento dei dati:', error));
  },
  methods: {
    filterLinks() {
      // Filtra i link in base alla parola chiave inserita
      this.filteredLinks = this.links.filter(link => 
        link.title.toLowerCase().includes(this.searchQuery.toLowerCase()) ||
        link.description.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
    }
  }
}
</script>



<template>
    <div>
        <!-- Barra di testo per inserire la parola chiave -->
        <input type="text" v-model="searchQuery" placeholder="Cerca..." @input="filterLinks" />

        <!-- Contenitore per le cards filtrate -->
        <div class="links-container">
            <div v-for="link in filteredLinks" :key="link.id" class="card">
                <h3>{{ link.title }}</h3>
                <p>{{ link.description }}</p>
                <a :href="link.url" target="_blank">Visita</a>
            </div>
        </div>
    </div>
</template>


<style></style>