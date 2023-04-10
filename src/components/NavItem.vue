<script setup>
const props = defineProps({
  item: Object,
});
</script>

<template>
  <a class="flex" :href="item.href">{{ item.label }}</a>

  <div class="ml-2" v-if="item.children.length">
    <NavItem
      class="flex"
      v-for="child in item.children"
      :item="child"
      :key="child.label"/>
  </div>
</template>
