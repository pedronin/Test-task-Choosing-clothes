<script setup>
import { reactive } from "vue";

import { shopItems, wardrobeItems } from "./mocks";

import GeneralList from "./components/GeneralList.vue";
import SelectedList from "./components/SelectedList.vue";

const limits = {
  wardrobeItems: 6,
  shopItems: 1,
};

const selectedData = reactive({
  wardrobeItems: [],
  shopItems: [],
});

const selectItem = (item, groupName) => {
  if (selectedData[groupName].length >= limits[groupName]) {
    return;
  }

  selectedData[groupName].push(item);
};

const deselectItem = (item, groupName) => {
  selectedData[groupName] = selectedData[groupName].filter(
    ({ id }) => id !== item.id
  );
};

const toggleItem = ({ item, isSelected }, groupName) => {
  if (isSelected) {
    deselectItem(item, groupName);
  } else {
    selectItem(item, groupName);
  }
};
</script>

<template>
  <div class="wrapper">
    <SelectedList
      placeholder="selected wardrobe items"
      :max-count="limits.wardrobeItems"
      :items="selectedData.wardrobeItems"
      @item:deselect="deselectItem($event, 'wardrobeItems')"
    />

    <SelectedList
      placeholder="selected shop items"
      :max-count="limits.shopItems"
      :items="selectedData.shopItems"
      @item:deselect="deselectItem($event, 'shopItems')"
    />

    <GeneralList
      :items="wardrobeItems"
      :selected-items="selectedData.wardrobeItems"
      @item:toggle="toggleItem($event, 'wardrobeItems')"
    />

    <GeneralList
      :items="shopItems"
      :selected-items="selectedData.shopItems"
      @item:toggle="toggleItem($event, 'shopItems')"
    />
  </div>
</template>

<style scoped>
.wrapper {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-template-rows: 30% auto;
  gap: 20px;

  height: 100%;
}
</style>
