<script setup>
import { onBeforeUnmount, onMounted, ref } from "vue";

defineEmits(["open-booking"]);

const navItems = [
  { id: "top", href: "#top", label: "首页" },
  { id: "menu", href: "#menu", label: "菜单" },
  { id: "story", href: "#story", label: "关于屿" },
  { id: "visit", href: "#visit", label: "来这里" },
];

const isMenuOpen = ref(false);
const activeSection = ref("top");
let sectionObserver;

function toggleMenu() {
  isMenuOpen.value = !isMenuOpen.value;
}

function closeMenu() {
  isMenuOpen.value = false;
}

onMounted(() => {
  if (!("IntersectionObserver" in window)) return;

  const sections = document.querySelectorAll("main section[id]");
  sectionObserver = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          activeSection.value = entry.target.id;
        }
      });
    },
    { rootMargin: "-40% 0px -50%", threshold: 0 },
  );

  sections.forEach((section) => sectionObserver.observe(section));
});

onBeforeUnmount(() => sectionObserver?.disconnect());
</script>

<template>
  <header class="site-header" id="top">
    <a class="brand" href="#top" aria-label="屿 MORI 首页" @click="closeMenu">
      <span class="brand-mark" aria-hidden="true">屿</span>
      <span class="brand-copy">
        <strong>MORI</strong>
        <small>KITCHEN &amp; BAR</small>
      </span>
    </a>

    <button
      class="menu-toggle"
      :class="{ open: isMenuOpen }"
      type="button"
      aria-label="打开导航"
      :aria-expanded="isMenuOpen"
      @click="toggleMenu"
    >
      <span></span>
      <span></span>
    </button>

    <nav class="main-nav" :class="{ open: isMenuOpen }" aria-label="主导航">
      <a
        v-for="item in navItems"
        :key="item.id"
        :class="{ active: activeSection === item.id }"
        :href="item.href"
        @click="closeMenu"
      >
        {{ item.label }}
      </a>
    </nav>

    <button class="header-booking" type="button" @click="$emit('open-booking')">
      预订座位 <span>↗</span>
    </button>
  </header>
</template>
