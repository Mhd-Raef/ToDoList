<template>
    <div>
        <div v-for="(item, index) in items" :key="index">
            <list-item
                :item="item"
                class="item"
                @itemChanged="$emit('reloadList')"
            />
        </div>
    </div>
</template>

<script>
import listItem from './listItem.vue'
export default {
    components: { listItem },
    props: ['items']
}
</script>

<style scoped>
.item {
    background: #62a7c8;
    padding: 5px;
    margin-top: 5px;
    transition-duration: 250ms;
}
.item:hover,
.item:focus {
    background: #72b0ce;
}
</style>
