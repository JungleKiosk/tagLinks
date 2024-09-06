<!-- src/components/TagsBar.vue -->

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
    <div class="tags-bar text-dark">
        <span v-for="tag in tags" :key="tag.id" @click="filterByTag(tag.name)"
            :class="{ 'tag-active': selectedTag === tag.name, 'tag-inactive': selectedTag && selectedTag !== tag.name }"
            class="tag">
            {{ tag.name }}
        </span>
    </div>
</template>



<style scoped>
.tags-bar {
    margin: 16px 0;
    display: flex;
    gap: 10px;
}

.tag {
    cursor: pointer;
    background-color: #f0f0f0;
    padding: 5px 10px;
    border-radius: 5px;
    transition: background-color 0.3s;
}

.tag-active {
    background-color: #007bff;
    color: white;
}

.tag-inactive {
    background-color: #ddd;
}
</style>