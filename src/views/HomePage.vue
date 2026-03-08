<script setup>
const spin = () => alert('Hello')
</script>

<template>
  <main class="min-h-screen bg-[#0F172A] px-4 py-8 text-white sm:px-6 lg:px-8">
    <div class="mx-auto max-w-7xl">
      <header class="mb-8">
        <p class="text-xs font-semibold tracking-[0.3em] text-violet-400 uppercase">Project #4</p>
        <h1 class="mt-2 text-4xl font-black text-[#F8FAFC] sm:text-5xl">Anime Shuffler</h1>
        <p class="mt-2 max-w-3xl text-sm text-[#F8FAFC]/80">Spin the reel, request a random anime from Jinkan with VueUse useFech, 
          and learn how REST API's signal rate limiting with HTTP 429.
        </p>
      </header>

      <div class="grid gap-6 lg:grid-cols-[1.2fr_0.8fr]">
        <section class="space-y-5">
          <div class="rounded-3xl border border-[#14B8A6]/70 bg-[#0F172A] p-5 shadow-2xl shadow-[#14B8A6]/30 backdrop-blur-sm">
            <div class="flex flex-col gap-3 sm:flex-row sm:items-center sm:justify-between">
              <div>
                <h2 class="text-xl font-bold text-[#F8FAFC]">Roulette</h2>
                <p class="text-sm text-[#F8FAFC]/80">Pull the lever for your next random anime recommendation</p>
              </div>
              <button 
                type="button" 
                class="cursor-pointer rounded-full border border-[#14B8A6] bg-[#14B8A6] text-[#0F172A] hover:bg-[#14B8A6]/80 focus:outline-none focus:ring-2 focus:ring-[#14B8A6]/90 px-6 py-3 text-base font-black tracking-wide"
                @click="spin"
              >
              Spin
            </button>
            </div>
          </div>
        </section>
      </div>
    </div>
  </main>
</template>
