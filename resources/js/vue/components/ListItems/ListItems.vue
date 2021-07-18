<template>
  <div>
    <div v-for="(item, index) in items" :key="index">
      <list-item :item="item" v-on:itemChanged="$emit('reloadList')" />
    </div>
  </div>
</template>

<script>
import ListItem from "./ListItem/ListItem.vue";
export default {
  props: ["items"],
  components: {
    ListItem,
  },
};
</script>
