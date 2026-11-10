<script setup>
import { computed, ref } from "vue";

const filters = [
  { value: "all", label: "全部" },
  { value: "small", label: "先分享一点" },
  { value: "main", label: "热乎乎的主菜" },
  { value: "sweet", label: "留一点甜" },
];

const dishes = [
  {
    id: 1,
    category: "small",
    image: "https://images.unsplash.com/photo-1547592180-85f173990554?auto=format&fit=crop&w=900&q=85",
    alt: "炭烤茄子配芝麻酱",
    title: "炭火茄子",
    description: "芝麻酱 · 香菜油 · 一点脆米",
    price: "¥ 48",
    revealClass: "",
  },
  {
    id: 2,
    category: "main",
    image: "https://images.unsplash.com/photo-1544025162-d76694265947?auto=format&fit=crop&w=900&q=85",
    alt: "炭火烤牛排配时蔬",
    title: "炭火牛排",
    description: "云南小土豆 · 黑胡椒肉汁",
    price: "¥ 48",
    badge: "本季主角",
    featured: true,
    revealClass: "reveal-delay-1",
  },
  {
    id: 3,
    category: "small",
    image: "https://images.unsplash.com/photo-1559339352-11d035aa65de?auto=format&fit=crop&w=900&q=85",
    alt: "海盐黄油虾吐司",
    title: "黄油虾吐司",
    description: "海盐 · 青柠 · 香草",
    price: "¥ 68",
    revealClass: "reveal-delay-2",
  },
  {
    id: 4,
    category: "sweet",
    image: "https://images.unsplash.com/photo-1551024506-0bccd828d307?auto=format&fit=crop&w=900&q=85",
    alt: "焦糖海盐布丁",
    title: "焦糖海盐布丁",
    description: "香草 · 榛子脆 · 一点点海盐",
    price: "¥ 42",
    revealClass: "",
  },
  {
    id: 5,
    category: "main",
    image: "https://images.unsplash.com/photo-1515003197210-e0cd71810b5f?auto=format&fit=crop&w=900&q=85",
    alt: "时令海鲜意面",
    title: "番茄海鲜意面",
    description: "时令海鲜 · 小番茄 · 初榨橄榄油",
    price: "¥ 118",
    revealClass: "reveal-delay-1",
  },
  {
    id: 6,
    category: "sweet",
    image: "https://images.unsplash.com/photo-1565958011703-44f9829ba187?auto=format&fit=crop&w=900&q=85",
    alt: "奶油芝士蛋糕",
    title: "柑橘芝士蛋糕",
    description: "柑橘酱 · 开心果 · 酸奶油",
    price: "¥ 52",
    revealClass: "reveal-delay-2",
  },
];

const activeFilter = ref("all");
const filteredDishes = computed(() =>
  activeFilter.value === "all"
    ? dishes
    : dishes.filter((dish) => dish.category === activeFilter.value),
);
</script>

<template>
  <section class="menu-section section-pad" id="menu">
    <div class="section-heading reveal">
      <div>
        <p class="eyebrow"><span></span> THE MENU</p>
        <h2>今晚，想和谁<br /><em>一起好好吃饭？</em></h2>
      </div>
      <p class="section-intro">
        我们把当季的好食材，做成一桌热气腾腾的心意。<br />慢慢吃，慢慢聊，今天也要好好照顾自己。
      </p>
    </div>

    <div class="menu-tabs reveal" role="tablist" aria-label="菜单分类">
      <button
        v-for="filter in filters"
        :key="filter.value"
        class="tab-button"
        :class="{ active: activeFilter === filter.value }"
        type="button"
        role="tab"
        :aria-selected="activeFilter === filter.value"
        @click="activeFilter = filter.value"
      >
        {{ filter.label }}
      </button>
      <span class="menu-date">今晚有好菜 · 等你来</span>
    </div>

    <div class="menu-grid">
      <article
        v-for="dish in filteredDishes"
        :key="dish.id"
        class="dish-card reveal"
        :class="[dish.revealClass, { 'featured-dish': dish.featured }]"
      >
        <div class="dish-image">
          <img :src="dish.image" :alt="dish.alt" loading="lazy" />
          <span class="dish-number">{{ String(dish.id).padStart(2, "0") }}</span>
          <span v-if="dish.badge" class="dish-badge">{{ dish.badge }}</span>
        </div>
        <div class="dish-info">
          <div>
            <h3>{{ dish.title }}</h3>
            <p>{{ dish.description }}</p>
          </div>
          <strong>{{ dish.price }}</strong>
        </div>
      </article>
    </div>

    <div class="menu-foot reveal">
      <p>菜单会随季节变化，剩下的，就交给今晚的好心情。</p>
      <a class="text-link" href="#visit">选一杯喜欢的酒 <span>↗</span></a>
    </div>
  </section>
</template>
