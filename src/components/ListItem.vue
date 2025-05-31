<script setup>
defineOptions({
  name: "ListItem",
});

const { name, selected } = defineProps({
  name: String,
  selected: Boolean,
});
</script>

<template>
  <li class="item" :class="{ 'item--selected': selected }">
    {{ name }}
  </li>
</template>

<style scoped lang="scss">
.item {
  position: relative;

  display: flex;
  align-items: center;
  justify-content: center;

  padding: 25px 5px;

  border: 3px solid #000;
  cursor: pointer;

  font-size: 20px;
  user-select: none;

  &--selected {
    &::after {
      content: "";

      position: absolute;
      top: 0;
      right: -5px;

      width: 30px;
      height: 30px;

      background-image: url("/icons/check.svg");
      background-size: 30px;
    }
  }
}
</style>
