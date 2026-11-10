<script setup>
defineEmits(["open-booking"]);
</script>

<template>
  <section class="hero section-pad">
    <div class="hero-copy reveal">
      <p class="eyebrow"><span></span> 珠江边 · 广州</p>
      <h1>把一餐，<br /><em>吃成一段好时光。</em></h1>
      <p class="hero-description">
        一间藏在城市缝隙里的餐厅。我们跟着季节选食材，跟着客人的心情调酒，留一张桌子给每一个值得庆祝的晚上。
      </p>
      <div class="hero-actions">
        <button class="button button-dark" type="button" @click="$emit('open-booking')">
          预订今晚的座位 <span>↗</span>
        </button>
        <a class="text-link" href="#menu">看看今天吃什么 <span>↓</span></a>
      </div>
      <div class="hero-meta">
        <div class="meta-item">
          <strong>12:00—23:00</strong>
          <span>周一至周日</span>
        </div>
        <div class="meta-divider"></div>
        <div class="meta-item">
          <strong>海珠区 · 太古仓</strong>
          <span>距江边 180m</span>
        </div>
      </div>
    </div>

    <div class="hero-visual reveal reveal-delay-1">
      <div class="hero-image image-frame">
        <img
          src="https://images.unsplash.com/photo-1515003197210-e0cd71810b5f?auto=format&fit=crop&w=1200&q=88"
          alt="餐桌上的精致菜肴与餐具"
        />
      </div>
      <div class="hero-stamp" aria-hidden="true">
        <span>GOOD FOOD</span>
        <strong>好好吃饭</strong>
        <span>GOOD MOOD</span>
      </div>
      <div class="hero-note">
        <span class="note-line"></span>
        <span>从一杯自然酒开始</span>
      </div>
    </div>
  </section>
</template>
