<script setup>
import NavItem from "../components/NavItem.vue";
import { HomeIcon, NewspaperIcon, PhotoIcon } from "@heroicons/vue/24/outline";             // Imports for the icons that I use in the array of objects below.

const navItems = [
  { href: "#", label: "Home", children: [], icon: HomeIcon, active: true },                 // Creation of an array of object. Each object represents an item in the menu.                    
  {                                                                                         //Each object have a children propertie than may or may not contain more objects of the
    href: "#",                                                                              //same style. Those objects, also represent submenu items of their parent element.
    label: "Post",  
    children: [
      { href: "#", label: "All post", children: [], icon: null, active: false },
      { href: "#", label: "Add new", children: [], icon: null, active: false },
      {
        href: "#",
        label: "Categories",
        children: [],
        icon: null,
        active: false,
      },
    ],
    icon: NewspaperIcon,
    active: false,
  },
  {
    href: "#",
    label: "Media",
    children: [
      { href: "#", label: "Library", children: [], icon: null, active: false },
      {
        href: "#",
        label: "Add new",
        children: [
          {
            href: "#",
            label: "Third level",
            children: [],
            icon: null,
            active: false,
          },
        ],
        icon: null,
        active: false,
      },
    ],
    icon: PhotoIcon,
    active: false,
  },
];
</script>

<template>
  <div class="flex min-h-screen">
    <div class="w-64 shrink-0 bg-gray-50 border-r border-gray-200 py-4">                <!-- Logo prefix-->
      <div class="px-4">
        <a href="#" class="inline-block">
          <img
            class="h-8 w-auto"
            src="../assets/vue.svg"
            alt="Logo"
            title="vueLogo"
          />
        </a>
      </div>
      <nav class="mt-2 px-2">                                                               <!-- Navigation part of the component, here I use a component that handles how the menu-->
        <NavItem :item="item" v-for="item in navItems" :key="item.label">                   <!--is render on the menu. Keep in mind that I'm using a v-for to map the array of objects-->
        </NavItem>                                                                          <!--above, and I'm also passing down as a prop in the :item propertie, each iteration of that-->
      </nav>                                                                                <!--v-for-->
    </div>
    <main class="p-4">content</main>                                                        <!--Here goes the main content of the page-->
  </div>
</template>
