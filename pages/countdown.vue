<template>
  <div class="tw-bg-gray-100 tw-min-h-screen tw-flex tw-justify-center tw-items-center">
    <div class="tw-max-w-lg tw-rounded-lg tw-shadow-lg tw-bg-white tw-p-8">
      <h1 class="tw-text-3xl tw-font-bold tw-text-center tw-mb-4">WAIT FOR IT!!</h1>
      <div class="tw-flex tw-justify-center tw-items-center tw-mb-4">
        <!-- <div class="tw-flex tw-items-center tw-text-2xl tw-font-bold">
          <div class="tw-p-2 tw-rounded-full tw-bg-gray-300 tw-mr-2" v-if="timeRemaining.days">{{ timeRemaining.days }}</div>
          <span v-else>0</span>
          <span class="tw-ml-1">Days</span>
        </div>
        <span class="tw-mx-4 tw-text-2xl">:</span> -->
        <div class="tw-flex tw-items-center tw-text-2xl tw-font-bold">
          <div class="tw-p-2 tw-rounded-full tw-bg-gray-300 tw-mr-2" v-if="timeRemaining.hours">{{ timeRemaining.hours }}
          </div>
          <span v-else>0</span>
          <span class="tw-ml-1">Hours</span>
        </div>
        <span class="tw-mx-4 tw-text-2xl">:</span>
        <div class="tw-flex tw-items-center tw-text-2xl tw-font-bold">
          <div class="tw-p-2 tw-rounded-full tw-bg-gray-300 tw-mr-2" v-if="timeRemaining.minutes">{{ timeRemaining.minutes
          }}</div>
          <span v-else>0</span>
          <span class="tw-ml-1">Minutes</span>
        </div>
        <span class="tw-mx-4 tw-text-2xl">:</span>
        <div class="tw-flex tw-items-center tw-text-2xl tw-font-bold">
          <div class="tw-p-2 tw-rounded-full tw-bg-gray-300 tw-mr-2" v-if="timeRemaining.seconds">{{ timeRemaining.seconds
          }}</div>
          <span v-else>0</span>
          <span class="tw-ml-1">Seconds</span>
        </div>
      </div>
      <p class="tw-text-lg tw-font-medium tw-text-center">NOTE!!!!</p>
      <p class="tw-text-lg tw-font-medium tw-text-center">VIDEO KA BAGO MO I CLICK ANG "GO!"</p>
      <div
        class="tw-p-2 tw-flex tw-content-center tw-justify-center tw-rounded-xl tw-border-4 tw-border-green-500 tw-bg-green-500">
        <NuxtLink to="/">
          <p class="tw-text-xl tw-font-medium"> GO!!</p>
        </NuxtLink>
      </div>

    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue';

// Set the target date (February 14, 2024) in Philippines time
const targetDate = new Date('2024-02-14T00:00:00+08:00').getTime();

// Countdown calculation
const now = ref(new Date().getTime());

const timeRemaining = computed(() => {
  const difference = targetDate - now.value;
  return {
    days: Math.floor(difference / (1000 * 60 * 60 * 24)),
    hours: Math.floor((difference % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60)),
    minutes: Math.floor((difference % (1000 * 60 * 60)) / (1000 * 60)),
    seconds: Math.floor((difference % (1000 * 60)) / 1000)
  };
});

// Update countdown every second
const intervalId = setInterval(() => {
  now.value = new Date().getTime();
}, 1000);

onMounted(() => {
  // Clear interval when component is unmounted
  return () => clearInterval(intervalId);
});
</script>

<style scoped>/* Add your custom styles here */</style>
