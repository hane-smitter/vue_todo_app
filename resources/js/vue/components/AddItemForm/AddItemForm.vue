<template>
    <div class="add-item">
        <input
            type="text"
            v-model="item.name"
            placeholder="Type todo"
        />
        <font-awesome-icon
            icon="plus-square"
            :class="[item.name ? 'active' : 'inactive', 'plus']"
            @click="add()"
        />
    </div>
</template>

<script>
export default {
    data: function() {
        return {
            item: {
                name: ""
            }
        }
    },
    methods: {
        add() {
            if(this.item.name.length < 1) return;
            axios.post('/api/item/store', {
                item: this.item
            })
            .then(response => {
                if(response.status == 201) this.item.name = "";
            })
            .catch(err => {
                console.log(err);
            });
        }
    }
}
</script>
<style scoped>
.add-item {
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #e6e6e6;
    padding: 5px 5px 5px 5px;
}
input {
    border: none;
    border-radius: 4px;
    outline: none;
    margin-right: 5px;
    background-color: #f7f7f7;
    padding: 5px;
    width: 100%;
}
.plus { font-size: 20px; }
.active { color: #00ce25; }
.inactive { color: #999999; }
</style>
