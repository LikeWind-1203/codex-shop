<script setup>
import { computed, nextTick, onBeforeUnmount, reactive, ref, watch } from "vue";

const props = defineProps({
  open: {
    type: Boolean,
    default: false,
  },
});

const emit = defineEmits(["close", "submitted"]);
const firstInput = ref(null);
const form = reactive({
  name: "",
  phone: "",
  date: "",
  time: "18:00",
  guests: "2 位",
});

const minimumDate = computed(() => {
  const today = new Date();
  const localDate = new Date(today.getTime() - today.getTimezoneOffset() * 60000);
  return localDate.toISOString().split("T")[0];
});

function resetForm() {
  form.name = "";
  form.phone = "";
  form.date = "";
  form.time = "18:00";
  form.guests = "2 位";
}

function closeModal() {
  emit("close");
}

function submitBooking() {
  emit("submitted", {
    name: form.name,
    date: form.date,
    time: form.time,
  });
  resetForm();
}

watch(
  () => props.open,
  (isOpen) => {
    document.body.classList.toggle("modal-open", isOpen);
    if (isOpen) {
      nextTick(() => firstInput.value?.focus());
    }
  },
  { immediate: true },
);

onBeforeUnmount(() => {
  document.body.classList.remove("modal-open");
});
</script>

<template>
  <div
    class="booking-modal"
    :class="{ open }"
    role="dialog"
    aria-modal="true"
    aria-labelledby="booking-title"
    :aria-hidden="!open"
  >
    <div class="modal-backdrop" @click="closeModal"></div>
    <div class="modal-panel">
      <button class="modal-close" type="button" aria-label="关闭预订窗口" @click="closeModal">×</button>
      <p class="eyebrow"><span></span> RESERVE A TABLE</p>
      <h2 id="booking-title">把今晚的好位置，<em>留给你。</em></h2>
      <p class="modal-description">告诉我们你的用餐计划，我们会在 15 分钟内与您确认。</p>
      <form class="booking-form" @submit.prevent="submitBooking">
        <label>
          姓名
          <input ref="firstInput" v-model="form.name" type="text" name="name" placeholder="怎么称呼你？" required />
        </label>
        <label>
          手机
          <input v-model="form.phone" type="tel" name="phone" placeholder="方便联系的号码" required />
        </label>
        <div class="form-row">
          <label>
            日期
            <input v-model="form.date" type="date" name="date" :min="minimumDate" required />
          </label>
          <label>
            时间
            <select v-model="form.time" name="time">
              <option>18:00</option>
              <option>18:30</option>
              <option>19:00</option>
              <option>19:30</option>
              <option>20:00</option>
              <option>20:30</option>
            </select>
          </label>
        </div>
        <label>
          人数
          <select v-model="form.guests" name="guests">
            <option>2 位</option>
            <option>3 位</option>
            <option>4 位</option>
            <option>5 位</option>
            <option>6 位及以上</option>
          </select>
        </label>
        <button class="button button-dark submit-booking" type="submit">提交预订 <span>↗</span></button>
      </form>
    </div>
  </div>
</template>
