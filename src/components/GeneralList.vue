<script setup>
import ListItem from "./ListItem.vue";

defineOptions({
  name: "GeneralList",
});

const { items, selectedItems } = defineProps({
  items: Array,
  selectedItems: Array,
});

const emits = defineEmits(["item:toggle"]);

const isSelected = (itemId) => {
  return selectedItems.some((item) => item.id === itemId);
};

const onClick = (item) => {
  emits("item:toggle", { item, isSelected: isSelected(item.id) });
};
</script>

<template>
  <ul class="general-list">
    <ListItem
      v-for="item in items"
      :key="item.id"
      :name="item.name"
      :selected="isSelected(item.id)"
      @click="onClick(item)"
    />
  </ul>
</template>

<style scoped lang="scss">
.general-list {
  display: grid;
  grid-template-columns: repeat(auto-fit, 100px);
  grid-auto-rows: min-content;
  gap: 4px;

  padding: 10px;

  border: 4px solid #000;
}
</style>
