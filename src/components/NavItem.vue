<script setup>
import { Disclosure, DisclosureButton, DisclosurePanel } from "@headlessui/vue";
import { ChevronDownIcon } from "@heroicons/vue/24/outline";
const props = defineProps({
  item: Object,
});

console.log(props.item);
</script>

<template>
  <a
    v-if="!item.children.length"
    :class="[
      'flex w-full items-center py-2 px-3 text-sm font-medium text-gray-600',
    ]"
    :href="item.href"
  >
    <component
      :class="['w-6 h-6 shrink-0 mr-2']"
      :is="item.icon"
      v-if="item.icon"
    ></component>
    <span>{{ item.label }}</span>
  </a>

  <Disclosure v-else>
    <DisclosureButton
      :class="[
        'flex w-full items-center py-2 px-3 text-sm font-medium text-gray-600' ,
      ]"
    >
      <component
        :class="['w-6 h-6 shrink-0 mr-2']"
        :is="item.icon"
        v-if="item.icon"
      ></component>
      <span class="flex-1 text-left">{{ item.label }}</span>
      <ChevronDownIcon :class="['w-6 h-6 shrink-0']" />
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
