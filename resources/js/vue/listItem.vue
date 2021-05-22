<template>
    <div class="item">
        <input
            type="checkbox"
            @change="updateCheck()"
            v-model="item.completed"
        />
        <span :class="[item.completed ? 'completed' : '', 'text']">
            {{item.name}}
        </span>
        <span>{{showDate()}}</span>

        <button @click="removeItem()" class="trashCan" >
            <font-awesome-icon icon="trash" />
        </button>
    </div>
</template>

<script>
export default {
    props: ['item'],
    methods: {
        updateCheck() {
            axios.put('api/item/' + this.item.id, {
                item: this.item
            })
            .then((result) => {
                if(result.status == 200 ){
                    this.$emit('itemChanged')
                }
            }).catch((err) => {
                console.log(err)
            });
        },
        removeItem() {
            axios.delete('api/item/' + this.item.id)
            .then((result) => {
                if(result.status == 200) {
                    this.$emit('itemChanged')
                }
            }).catch((err) => {
                console.log(err)
            });
        },
        showDate() {
            const itemDate = new Date(this.item.created_at)
            return itemDate.getMonth() +'/'+ itemDate.getDay() + ' ' + itemDate.getHours()+':'+itemDate.getMinutes()+':'+itemDate.getSeconds()
        }
    }
}
</script>

<style scoped>
.completed {
    text-decoration: line-through;
    color: #555;
}
.text {
    width: 100%;
    margin-left: 20px;
}
.item {
    display: flex;
    justify-content: center;
    align-items: center;
    border: none;
    border-radius: 10px;
}

input[type='checkbox']{
    display: inline-block;
    width: 20px;
}
.trashCan{
    background: none;
    border: none;
    color: #ff0000;
    outline: none;
    cursor: pointer;
    transition-duration: 250ms;
    margin-left: 5px;
}
.trashCan:hover,
.trashCan:focus
{
    color: #ff4d4d;
}
</style>
