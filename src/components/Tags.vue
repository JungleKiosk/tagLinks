<!-- src/components/TagsBar.vue -->
<script>
export default {
    name: 'TagsBar',
    props: {
        tags: Array // Riceve le tag come proprietà dal componente padre
    },
    methods: {
        filterByTag(tag) {
            this.$emit('tag-selected', tag); // Emette un evento al clic su una tag
        }
    }
}
</script>


<template>
    <div class="tags-bar text-dark">
        <span v-for="tag in tags" :key="tag.id" @click="filterByTag(tag.name)" class="tag">
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
}
</style>