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
        <div class="tags-bar text-dark mb-3 ">
            <span v-for="tag in tags" :key="tag.id" @click="filterByTag(tag.name)"
                :class="{ 'tag-active': selectedTag === tag.name, 'tag-inactive': selectedTag && selectedTag !== tag.name }"
                class="tag rounded-pill">
                {{ tag.name }}
            </span>
        </div>
    </div>


</template>



<style scoped>

</style>