<script setup>
defineEmits(["open-booking"]);
</script>

<template>
  <section class="visit-section section-pad" id="visit">
    <div class="visit-card reveal">
      <div class="visit-content">
        <p class="eyebrow"><span></span> COME SAY HI</p>
        <h2>来江边，<br /><em>一起吃顿饭。</em></h2>
        <div class="visit-details">
          <div>
            <span>地址</span>
            <strong>广州市海珠区革新路 124 号<br />太古仓码头 A 栋 2F</strong>
          </div>
          <div>
            <span>营业时间</span>
            <strong>午市 12:00—14:30<br />晚市 17:30—23:00</strong>
          </div>
          <div>
            <span>联系</span>
            <strong>020 — 8421 1314<br />hello@mori-kitchen.cn</strong>
          </div>
        </div>
        <button class="button button-light" type="button" @click="$emit('open-booking')">
          预订座位 <span>↗</span>
        </button>
      </div>
      <div class="map-art" aria-label="餐厅位置示意图" role="img">
        <div class="map-water"></div>
        <div class="map-road road-one"></div>
        <div class="map-road road-two"></div>
        <div class="map-road road-three"></div>
        <div class="map-block block-one"></div>
        <div class="map-block block-two"></div>
        <div class="map-block block-three"></div>
        <div class="map-pin"><span>屿</span></div>
        <div class="map-label">TAIKOO WHARF<br /><small>太古仓</small></div>
        <div class="map-compass">N<br /><span>↑</span></div>
      </div>
    </div>
  </section>
</template>
