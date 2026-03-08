<script setup>
  const props = defineProps({
    anime: {
      type: Object,
      default: null,
    },
    loading: {
      type: Boolean,
      default: false,
    },
    error: {
      type: String,
      default: '',
    },
    inWatchlist: {
      type: Boolean,
      default: false,
    },
  })
</script>
<template>
  <section class="rounded-3xl border border-[#14B8A6]/70 bg-[#0F172A] p-5 shadow-2xl shadow-[#14B8A6]/30 backdrop-blur-sm">
    <div 
      v-if="props.loading"
      class="space-y-4"
    >
      <div class="flex items-center gap-3 text-[#F8FAFC]">
        <div class="h-5 w-5 animate-spin rounded-full border-2 border-[#14B8A6] border-t-transparent"></div>
        <p class="font-semibold tracking-wide">Shuffling anime reels...</p>
      </div>

      <div class="grid grid-cols-3 gap-2">
        <div class="h-3 animate-pulse rounded bg-[#14B8A6]"></div>
        <div class="h-3 animate-pulse rounded bg-[#14B8A6]"></div>
        <div class="h-3 animate-pulse rounded bg-[#14B8A6]"></div>
      </div>
      <div class="h-72 animate-pulse rounded-2xl bg-[#14B8A6]"></div>
    </div>

    <div v-else>Done</div>
  </section>
</template>