<script setup>
import { Disclosure, DisclosureButton, DisclosurePanel } from "@headlessui/vue";

const props = defineProps({
  item: Object,
});
</script>

<template>
  <a v-if="!item.children.length" class="flex" :href="item.href">{{ item.label }}</a>

  <Disclosure v-else>
    <DisclosureButton class="flex">
      {{item.label}}
    </DisclosureButton>
    <DisclosurePanel class="ml-4">
        <NavItem
        v-for="child in item.children"
        :item="child"
        :key="child.label"
      />
    </DisclosurePanel>
  </Disclosure>
</template>
