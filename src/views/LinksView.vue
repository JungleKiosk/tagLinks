<script>
import { tags } from '../data/tagsData'; // Importa le tag dal file tagsData.js
import Tags from '../components/Tags.vue'; // Importa il componente Tags

export default {
    name: 'LinksView',
    components: {
        Tags
    },
    data() {
        return {
            searchQuery: '',
            links: [],
            filteredLinks: [],
            tags, // Aggiungi le tag al data del componente
            selectedTag: ''
        };
    },
    created() {
        fetch('/src/data/data.json')
            .then(response => response.json())
            .then(data => {
                this.links = data;
                this.filteredLinks = data;
            })
            .catch(error => console.error('Errore nel caricamento dei dati:', error));
    },
    methods: {
        filterLinks() {
            const query = this.searchQuery.toLowerCase();
            this.filteredLinks = this.links.filter(link =>
                (link.title.toLowerCase().includes(query) || link.description.toLowerCase().includes(query)) &&
                (!this.selectedTag || link.description.toLowerCase().includes(this.selectedTag.toLowerCase()))
            );
        },
        filterByTag(tag) {
            this.selectedTag = tag;
            this.filterLinks(); // Aggiorna il filtraggio quando una tag viene selezionata
        }
    }
}
</script>


<template>
    <div>
        <!-- Barra di testo per inserire la parola chiave -->
        <input type="text" v-model="searchQuery" placeholder="Cerca..." @input="filterLinks" />

        <!-- Componente Tags per filtrare con le tag -->
        <Tags :tags="tags" @tag-selected="filterByTag" />

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