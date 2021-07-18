<template>
  <div class="item">
    <input type="checkbox" @change="updateCheck()" v-model="item.completed" />
    <span :class="[item.completed ? 'completed' : '', 'itemText']">
      {{ item.name }}
    </span>
    <font-awesome-icon
        icon='trash'
        class="trashcan"
    />
  </div>
</template>

<script>
export default {
  props: ["item"],
  methods: {
    updateCheck() {
      axios.patch("/api/item/" + this.item.id, {
          item: {
              completed: this.item.completed ? true : false
          }
      })
      .then(response => {
          if(response.status == 200) this.$emit('itemChanged');
      })
      .catch(err => console.log(err));
    },
  },
};
</script>
<style scoped>
.completed {
  text-decoration: line-through;
  color: #999999;
}
.itemText {
  width: 100%;
  margin-left: 20px;
}
.item {
  display: flex;
  justify-content: center;
  align-items: center;
}
.trashcan {
  border: none;
  background: #e6e6e6;
  outline: none;
  color: #ff0000;
}
</style>
