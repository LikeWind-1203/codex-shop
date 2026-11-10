<script setup>
import { onBeforeUnmount, onMounted, ref } from "vue";
import BookingModal from "./components/BookingModal.vue";
import ExperienceSection from "./components/ExperienceSection.vue";
import HeroSection from "./components/HeroSection.vue";
import MenuSection from "./components/MenuSection.vue";
import MarqueeBand from "./components/MarqueeBand.vue";
import SiteFooter from "./components/SiteFooter.vue";
import SiteHeader from "./components/SiteHeader.vue";
import StorySection from "./components/StorySection.vue";
import ToastMessage from "./components/ToastMessage.vue";
import VisitSection from "./components/VisitSection.vue";
import { useRevealObserver } from "./composables/useRevealObserver.js";

const isBookingOpen = ref(false);
const isToastVisible = ref(false);
const toastMessage = ref("");
let toastTimer;

useRevealObserver();

function openBooking() {
  isBookingOpen.value = true;
}

function closeBooking() {
  isBookingOpen.value = false;
}

function showToast(message) {
  toastMessage.value = message;
  isToastVisible.value = true;
  window.clearTimeout(toastTimer);
  toastTimer = window.setTimeout(() => {
    isToastVisible.value = false;
  }, 4500);
}

function handleBookingSubmitted({ name, date, time }) {
  closeBooking();
  showToast(`${name}，已收到你 ${date} ${time} 的预订请求，我们马上联系你。`);
}

function handleEscape(event) {
  if (event.key === "Escape" && isBookingOpen.value) {
    closeBooking();
  }
}

onMounted(() => {
  document.addEventListener("keydown", handleEscape);
});

onBeforeUnmount(() => {
  document.removeEventListener("keydown", handleEscape);
  window.clearTimeout(toastTimer);
});
</script>

<template>
  <div class="site-shell">
    <SiteHeader @open-booking="openBooking" />

    <main>
      <HeroSection @open-booking="openBooking" />
      <MarqueeBand />
      <MenuSection />
      <StorySection />
      <ExperienceSection />
      <VisitSection @open-booking="openBooking" />
    </main>

    <SiteFooter />
  </div>

  <BookingModal
    :open="isBookingOpen"
    @close="closeBooking"
    @submitted="handleBookingSubmitted"
  />
  <ToastMessage :message="toastMessage" :visible="isToastVisible" />
</template>
