<template>
    <div class="TodoListContainer">
        <div class="heading">
            <h2 id="title">Todo List</h2>
            <add-item
                @reloadList="getItems()"
            />
        </div>
        <list-view
            :items="items"
            @reloadList="getItems()"
        />

        <div class="delete" @click="remove()" v-if="items.length">
            Delete all tasks
        </div>
    </div>
</template>

<script>
import AddItem from './addItem.vue'
import ListView from './listView.vue'

export default {
    components: {
        AddItem,
        ListView
    },
    data() {
        return {
            items: []
        }
    },
    methods: {
        getItems() {
            axios.get('api/items')
            .then((res) => {
                this.items = res.data
            }).catch((err) => {
                console.log(err)
            });
        },
        remove() {
            axios.delete('api/item/')
            .then((result) => {
                if(result.status == 200) {
                    this.getItems()
                }
            }).catch((err) => {
                console.log(err)
            });
        }
    },
    created() {
        this.getItems()
    }
}
</script>

<style scoped>
    .TodoListContainer {
        width: 350px;
        margin: auto;
        color: #eee;
    }
    .heading {
        background: #1e81b0;
        padding: 10px;
        border: none;
        border-radius: 10px;
    }
    #title {
        text-align: center;
    }
    .delete {
        width: 350px;
        margin: 20px auto;
        text-align: center;
        border: none;
        border-radius: 10px;
        background: #be2530;
        padding: 10px 0px;
        cursor: pointer;
        transition-duration: 250ms;
    }
    .delete:hover,
    .delete:focus {
        background: #c53b45;
    }
</style>
