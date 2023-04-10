<script setup>
import NavItem from "../components/NavItem.vue";
import { HomeIcon, NewspaperIcon, PhotoIcon } from "@heroicons/vue/24/outline";

const navItems = [
  { href: "#", label: "Home", children: [], icon: HomeIcon, active: true },
  {
    href: "#",
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
    <div class="w-64 shrink-0 bg-gray-50 border-r border-gray-200 py-4">
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
      <nav class="mt-2 px-2">
        <NavItem :item="item" v-for="item in navItems" :key="item.label">
        </NavItem>
      </nav>
    </div>
    <main class="p-4">content</main>
  </div>
</template>
