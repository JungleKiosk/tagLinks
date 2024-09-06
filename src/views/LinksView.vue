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
            tags,
            selectedTag: '' // Stato per la tag selezionata
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
        onSearchInput() {
            // Disattiva la tag selezionata quando viene digitato qualcosa nella barra di ricerca
            this.selectedTag = '';
            this.filterLinks();
        },
        filterLinks() {
            const query = this.searchQuery.toLowerCase();
            this.filteredLinks = this.links.filter(link =>
                (link.title.toLowerCase().includes(query) || link.description.toLowerCase().includes(query)) &&
                (!this.selectedTag || link.tags.includes(this.selectedTag))
            );
        },
        filterByTag(tag) {
            // Disattiva la ricerca quando una tag viene selezionata
            this.searchQuery = '';
            this.selectedTag = tag; // Imposta la tag selezionata
            this.filterLinks(); // Aggiorna il filtraggio
        }
    }
}
</script>

<template>
    <div class="container">
        <div class="row sticky-container p-5">
            <div class="col-12">
                <input type="text" v-model="searchQuery" placeholder="Cerca..." @input="onSearchInput" />
            </div>
            <div class="col-12">
                <Tags :tags="tags" :selectedTag="selectedTag" @tag-selected="filterByTag" />
            </div>
        </div>
        <!-- Barra di testo per inserire la parola chiave -->

        <!-- Componente Tags per filtrare con le tag -->
        <div class="row">
            <div class="col-12">
                <div class="links-container">
                    <div v-for="link in filteredLinks" :key="link.id" class="card bg-secondary text-dar mb-5">
                        <h3>{{ link.title }}</h3>
                        <p>{{ link.description }}</p>
                        <a class="text-warning" :href="link.url" target="_blank">Visita</a>
                        <!-- Visualizza le tag della card -->
                        <div class="card-tags">
                            <span v-for="tag in link.tags" :key="tag" class="card-tag">
                                {{ tag }}
                            </span>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <!-- Contenitore per le cards filtrate -->
    </div>
</template>


<style scoped>
.sticky-container {
    position: sticky;
    top: 0;
    z-index: 1000;
    display: flex;
    background-color: #1d1d1d;
}
</style>
