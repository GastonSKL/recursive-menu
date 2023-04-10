<script setup>
import { Disclosure, DisclosureButton, DisclosurePanel } from "@headlessui/vue";        // Here I import the headlessui components. This allows me to have a collapsable menu component 
import { ChevronDownIcon } from "@heroicons/vue/24/outline";                            //for each menu item and it's childrens
import { computed } from "vue";
const props = defineProps({
  item: Object,
});

const activeChiled = computed(()=>{                                                     // This allow me to store the computed active state of each of the elements of the array in the main 
    function hasActiveItem(items){                                                      //component. With this I can know if an item is in it's active state and render the menu in the correct
        return items.some(item => item.active || hasActiveItem(item.children))          //way. For example, if a children of an object is active, this will make so that the correct path to
    }                                                                                   //that children is desplayed and colapsed, and no the entire three.
    return hasActiveItem(props.item.children)
})

</script>

<template>
  <a
    v-if="!item.children.length"
    :class="[
        'text-left group flex w-full items-center rounded-md py-2 px-3 text-sm font-medium text-gray-600',    // Here I display the current item that I'm iterating in the array of objects
        'hover:bg-gray-100',                                                                                    //with his respective icon, in case that it has one, in the component tag. Also   
        item.active ? 'text-gray-800 font-semibold' : 'text-gray-600 font-medium'                               //this manipulates the classes taht are aplied to this items based on the active status
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

  <Disclosure v-else v-slot="{ open }" :default-open="activeChiled">                                        <!--In here I use the headless ui components to give the dropdown functionality-->
    <DisclosureButton                                                                                       
      :class="[                                                                                             //In case that the item have childrens, it uses recursivity to display correctly
        'text-left group flex w-full items-center rounded-md py-2 px-3 text-sm font-medium text-gray-600',//the path to the children elements, and it manipulates the open substat of the 
        'hover:bg-gray-100',                                                                              //<Disclosure/> component that is passed throw the v-slot directive. In case that it's  
        open ? 'font-bold text-gray-800' : 'text-gray-600 font-medium',                                 //open it aplly certains classes and viceversa.
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
      />                                                                                                    <!--Arrow icon that changes direction in case of the open propertie is apllied-->
    </DisclosureButton>
    <DisclosurePanel class="ml-4">                                                                          <!--This map the entire children section of the element in case that it has one-->
      <NavItem
        v-for="child in item.children"
        :item="child"
        :key="child.label"
      />
    </DisclosurePanel>
  </Disclosure>
</template>
