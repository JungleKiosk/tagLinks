<script>
export default {
    name: 'TagsBar',
    props: {
        tags: Array,
        selectedTag: String //tag selezionata dal componente padre
    },
    methods: {
        filterByTag(tag) {
            if (this.selectedTag === tag) {
                this.$emit('tag-selected', ''); 
            } else {
                this.$emit('tag-selected', tag);
            }
        }
    }
}
</script>


<template>


    <div class="tags-bar-wrapper">
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