<script setup>
import { Disclosure, DisclosureButton, DisclosurePanel } from "@headlessui/vue";
import { ChevronDownIcon } from "@heroicons/vue/24/outline";
import { computed } from "vue";
const props = defineProps({
  item: Object,
});

const activeChiled = computed(()=>{
    function hasActiveItem(items){
        return items.some(item => item.active || hasActiveItem(item.children))
    }
    return hasActiveItem(props.item.children)
})

console.log(props.item);
</script>

<template>
  <a
    v-if="!item.children.length"
    :class="[
        'text-left group flex w-full items-center rounded-md py-2 px-3 text-sm font-medium text-gray-600',
        'hover:bg-gray-100',
        item.active ? 'text-gray-800 font-semibold' : 'text-gray-600 font-medium'
      ]"
    :href="item.href"
  >
    <component
      :class="[
        'w-6 h-6 shrink-0 mr-2  group-hover:text-gray-600',
        item.active ? 'text-gray-600' : 'text-gray-400'
      ]"
      :is="item.icon"
      v-if="item.icon"
    ></component>
    <span>{{ item.label }}</span>
  </a>

  <Disclosure v-else v-slot="{ open }" :default-open="activeChiled">
    <DisclosureButton
      :class="[
        'text-left group flex w-full items-center rounded-md py-2 px-3 text-sm font-medium text-gray-600',
        'hover:bg-gray-100',
        open ? 'font-bold text-gray-800' : 'text-gray-600 font-medium',
      ]"
    >
      <component
        :class="[
          'w-6 h-6 shrink-0 mr-2  group-hover:text-gray-600',
          open ? 'text-gray-600' : 'text-gray-400',
        ]"
        :is="item.icon"
        v-if="item.icon"
      ></component>
      <span class="flex-1 text-left">{{ item.label }}</span>
      <ChevronDownIcon
        :class="['w-6 h-6 shrink-0', open ? '-rotate-180 text-gray-600' : 'text-gray-400']"
      />
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
