<script setup>
import { computed, ref, watch } from 'vue'

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

  const emit = defineEmits(['add'])
  
  const synopsisExpanded = ref(false)

  const animeImage = computed(() => {
    return (
      props.anime?.images?.jpg?.large_image_url ||
      props.anime?.images?.jpg?.image_url ||
      props.anime?.images?.webp?.large_image_url ||
      props.anime?.images?.webp?.image_url ||
      ''
    )
  })

  const synopsis = computed(() => {
    return props.anime?.synopsis || 'No synopsis available.'
  })

  const needTruncation = computed(() => synopsis.value.length > 240)

  const visibleSynopsis = computed(() => {
    if (synopsisExpanded.value || !needTruncation.value) {
      return synopsis.value
    }
    return `${synopsis.value.slice(0, 240)}...`
  })

  watch(
    () => props.anime?.mal_id,
    () => {
      synopsisExpanded.value = false
    }
  )
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

    <div v-else-if="error"
      class="rounded-2xl border border-[#F59E0B]/90 bg-[#F59E0B]/50 p-4 text-black"
    >
      <h3 class="text-lg font-semibold">Spin failed</h3>
      <p class="mt-2 text-sm text-black">{{ error }}</p>  
    </div>

    <div 
      v-else-if="anime"
      class="space-y-4"
    >
      <div class="overflow-hidden rounded-2xl border border-slate-700/80 bg-slate-800/60">
        <img
          v-if="animeImage"
          :src="animeImage"
          :alt="anime.title"
          class="h-80 w-full bg-slate-900/50 object-contain"
          loading="lazy"
        />
      </div>

      <div>
        <h2 class="text-2xl font-black text-white">{{ anime.title }}</h2>
        <p class="mt-1 text-sm text-slate-300">
          Score: <span class="font-semibold text-amber-300">{{ anime.score ?? 'N/A' }}</span> •
          Episodes: <span class="font-semibold text-cyan-300">{{ anime.episodes ?? 'Unknown' }}</span> •
          Rating: <span class="font-semibold text-pink-300">{{ anime.rating || 'Unknown' }}</span>
        </p>
      </div>

      <p class="text-sm leading-relaxed text-slate-200">
        {{ visibleSynopsis }}
        <button
          v-if="needsTruncation"
          type="button"
          class="ml-2 text-cyan-300 underline-offset-4 hover:underline"
          @click="synopsisExpanded = !synopsisExpanded"
        >
          {{ synopsisExpanded ? 'Show less' : 'Read more' }}
        </button>
      </p>

      <div class="flex flex-wrap gap-3">
        <button
          type="button"
          class="rounded-full border border-cyan-300/60 bg-cyan-400/15 px-4 py-2 text-sm font-semibold text-cyan-100"
          :disabled="inWatchlist"
          @click="emit('add', anime)"
        >
          {{ inWatchlist ? 'In Watchlist' : 'Add to Watchlist' }}
        </button>

        <a
          :href="anime.url"
          target="_blank"
          rel="noopener noreferrer"
          class="rounded-full border border-white/20 px-4 py-2 text-sm font-semibold text-white transition hover:border-white/60"
        >
          Open on MAL
        </a>
      </div>
    </div>

    <div v-else>Done</div>
  </section>
</template>