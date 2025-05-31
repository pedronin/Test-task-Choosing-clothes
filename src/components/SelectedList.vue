<script setup>
import ListItem from "./ListItem.vue";

defineOptions({
  name: "SelectedList",
});

const { placeholder, items, hasCounter } = defineProps({
  items: Array,
  placeholder: String,
  maxCount: Number,
});

const emits = defineEmits(["item:deselect"]);
</script>

<template>
  <div class="selected-list">
    <template v-if="items.length">
      <ul class="selected-list__list">
        <ListItem
          v-for="item in items"
          :key="item.id"
          :name="item.name"
          @click="emits('item:deselect', item)"
        />
      </ul>

      <div class="selected-list__counter">
        Selected: {{ items.length }} / {{ maxCount }}
      </div>
    </template>

    <template v-else>
      <span class="selected-list__placeholder">{{ placeholder }}</span>
    </template>
  </div>
</template>

<style scoped lang="scss">
.selected-list {
  display: flex;
  flex-direction: column;

  padding: 10px;

  border: 4px solid #000;

  &__list {
    display: grid;
    grid-template-columns: repeat(auto-fit, 100px);
    gap: 4px;
  }

  &__counter {
    margin-top: auto;

    font-size: 22px;
    text-align: center;
  }

  &__placeholder {
    font-size: 22px;
    text-align: center;
  }
}
</style>
