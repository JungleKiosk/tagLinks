<template>
    <div>
        <!-- Barra di testo per inserire la parola chiave -->
        <input 
            type="text" 
            v-model="searchQuery" 
            placeholder="Cerca..." 
            @input="onSearchInput" 
        />

        <!-- Componente Tags per filtrare con le tag -->
        <Tags 
            :tags="tags" 
            :selectedTag="selectedTag" 
            @tag-selected="filterByTag" 
        />

        <!-- Contenitore per le cards filtrate -->
        <div class="links-container">
            <div 
                v-for="link in filteredLinks" 
                :key="link.id" 
                class="card bg-secondary text-dar"
            >
                <h3>{{ link.title }}</h3>
                <p>{{ link.description }}</p>
                <a class="text-warning" :href="link.url" target="_blank">Visita</a>
                <!-- Visualizza le tag della card -->
                <div class="card-tags">
                    <span 
                        v-for="tag in link.tags" 
                        :key="tag" 
                        class="card-tag"
                    >
                        {{ tag }}
                    </span>
                </div>
            </div>
        </div>
    </div>
</template>

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

.card-tags {
    margin-top: 8px;
}

.card-tag {
    display: inline-block;
    margin-right: 5px;
    background-color: #f0f0f0;
    padding: 3px 6px;
    border-radius: 4px;
    font-size: 12px;
}
</style>
