<template>
  <div class="todoContainer">
    <div class="heading">
      <h2 id="title">Todo List Application</h2>
    </div>
    <div>
      <div class="add-todo-form">
        <add-item-form />
      </div>
      <div class="todo-items">
        <list-items
            :items="items"
            v-on:reloadList="getToDos()"
        />
      </div>
    </div>
  </div>
</template>

<script>
import AddItemForm from "./components/AddItemForm/AddItemForm.vue";
import ListItems from "./components/ListItems/ListItems.vue";

export default {
  components: {
    AddItemForm,
    ListItems,
  },
  data() {
    return {
      items: [],
    };
  },
  methods: {
    getToDos() {
      axios
        .get("/api/items")
        .then((response) => {
            console.log(response.data);
            this.items = response.data
        })
        .catch((err) => console.log(err));
    },
  },
  created() {
    this.getToDos.call();
  },
};
</script>

<style scoped>
.todoContainer {
  width: 50vw;
  min-width: 400px;
  margin: 0 auto;
}
.heading {
  background-color: #e6e6e6;
  padding: 5px 5px 0px 5px;
}
#title {
  text-align: center;
  margin-bottom: 0;
}
</style>