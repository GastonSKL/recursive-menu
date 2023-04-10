<script setup>
const navItems = [
  { href: "#", label: "Home", children: [], icon: null },
  {
    href: "#",
    label: "Post",
    children: [
      { href: "#", label: "All post", children: [], icon: null },
      { href: "#", label: "Add new", children: [], icon: null },
      { href: "#", label: "Categories", children: [], icon: null },
    ],
    icon: null,
  },
  {
    href: "#",
    label: "Media",
    children: [
      { href: "#", label: "Library", children: [], icon: null },
      {
        href: "#",
        label: "Add new",
        children: [
          { href: "#", label: "Third level", children: [], icon: null },
        ],
        icon: null,
      },
    ],
    icon: null,
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
      <nav>
        <template v-for="item in navItems" :key="item.label">

                <a class="flex" :href="item.href">{{item.label}}</a>

                <div v-if="item.children.length">
                    <a class="flex ml-2" v-for="child in item.children" :key="child.label" :href="child.href">{{child.label}}</a>
                </div>

        </template>
        
      </nav>
    </div>
    <main class="p-4">content</main>
  </div>
</template>
