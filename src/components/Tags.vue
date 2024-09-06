<script>
export default {
    name: 'TagsBar',
    props: {
        tags: Array,
        selectedTag: String // Riceve la tag selezionata dal componente padre
    },
    methods: {
        filterByTag(tag) {
            if (this.selectedTag === tag) {
                this.$emit('tag-selected', ''); // Deseleziona se la stessa tag viene cliccata di nuovo
            } else {
                this.$emit('tag-selected', tag); // Altrimenti, seleziona la nuova tag
            }
        }
    }
}
</script>


<template>


    <div class="tags-bar-wrapper">
        <!-- Contenitore che contiene le tag e permette lo scorrimento orizzontale -->
        <div class="tags-bar text-dark">
            <span v-for="tag in tags" :key="tag.id" @click="filterByTag(tag.name)"
                :class="{ 'tag-active': selectedTag === tag.name, 'tag-inactive': selectedTag && selectedTag !== tag.name }"
                class="tag">
                {{ tag.name }}
            </span>
        </div>
    </div>


</template>



<style scoped>
/* Contenitore principale che racchiude la barra delle tag */
.tags-bar-wrapper {
    overflow-x: auto;
    /* Permette lo scorrimento orizzontale */
    white-space: nowrap;
    /* Impedisce la rottura delle linee */
    width: 100%;
    /* Adatta la larghezza al contenitore */
    margin-bottom: 16px;
}

/* Contenitore delle tag con stile Flexbox */
.tags-bar {
    display: flex;
    gap: 10px;
    padding: 8px;
}

/* Stili per le singole tag */
.tag {
    cursor: pointer;
    background-color: #f0f0f0;
    padding: 5px 10px;
    border-radius: 5px;
    transition: background-color 0.3s;
    display: inline-block;
    white-space: nowrap;
    /* Evita che il testo vada a capo */
}

/* Stile per la tag attiva */
.tag-active {
    background-color: #007bff;
    color: white;
}

/* Stile per le tag inattive */
.tag-inactive {
    background-color: #ddd;
}
</style>