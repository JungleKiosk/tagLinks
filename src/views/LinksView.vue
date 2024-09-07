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
            this.searchQuery = '';
            if (this.selectedTag === tag) {
                this.selectedTag = '';  // Deseleziona la tag se è già selezionata
            } else {
                this.selectedTag = tag; // Seleziona la nuova tag
            }
            this.filterLinks(); // Aggiorna il filtraggio
        }
    }

}
</script>

<template>
    <div class="container">
        <div class="row justify-content-center sticky-container mt-3">
            <div class="col-12 col-lg-8 mt-3 mb-3">
                <input class="search_bar rounded-pill p-2" type="text" v-model="searchQuery" placeholder="Enter a key word..." @input="onSearchInput" />
            </div>
            <div class="col-12 col-lg-8">
                <Tags :tags="tags" :selectedTag="selectedTag" @tag-selected="filterByTag" />
            </div>
            <a href="#header">Go up ^</a>
        </div>
        <!-- Barra di testo per inserire la parola chiave -->

        <!-- Componente Tags per filtrare con le tag -->
        <div class="row mt-5">
            <div class="col-12 col-lg-12">
                <div class="links-container">
                    <div v-for="link in filteredLinks" :key="link.id" class="card card_link p-3 text-dar mb-3">
                        <h3>{{ link.title }}</h3>
                        <p>{{ link.description }}</p>
                        <a class="text-warning" :href="link.url" target="_blank">View</a>
                        <!-- Visualizza le tag della card -->
                        <div class="">
                            <p>Tags:</p>
                            <span v-for="tag in link.tags" :key="tag" class="mx-2 card_tags btn rounded-pill">
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

</style>
