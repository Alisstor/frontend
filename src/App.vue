<script setup lang="ts">
import { onMounted, ref } from 'vue'
import api from './lib/api'

const backendStatus = ref('Checking connection...')
const backendMessage = ref('')

const checkBackend = async () => {
  try {
    const { data } = await api.get('/health')
    backendStatus.value = 'Connected locally'
    backendMessage.value = `${data.service} is ${data.status}`
  } catch (error) {
    backendStatus.value = 'Not connected'
    backendMessage.value = error instanceof Error ? error.message : 'Unknown error'
  }
}

onMounted(checkBackend)
</script>

<template>
  <main class="min-h-screen bg-slate-950 text-slate-50">
    <div class="mx-auto flex min-h-screen max-w-5xl items-center justify-center px-6 py-16">
      <div class="w-full max-w-xl rounded-2xl border border-slate-800 bg-slate-900/80 p-8 shadow-2xl ring-1 ring-slate-800/80 backdrop-blur-sm">
        <p class="mb-3 inline-flex rounded-full border border-violet-500/30 bg-violet-500/10 px-3 py-1 text-xs font-medium uppercase tracking-[0.2em] text-violet-300">
          Vue + Go local stack
        </p>
        <h1 class="text-4xl font-bold tracking-tight text-white">Frontend and backend are connected locally</h1>
        <p class="mt-4 text-base text-slate-300">
          The frontend uses env-based API configuration and Axios, with the Go backend running locally on port 8080.
        </p>

        <div class="mt-8 rounded-xl border border-slate-700 bg-slate-950/60 p-4">
          <p class="text-sm uppercase tracking-[0.2em] text-slate-400">Backend status</p>
          <p class="mt-2 text-xl font-semibold text-white">{{ backendStatus }}</p>
          <p class="mt-2 text-sm text-slate-300">{{ backendMessage || 'Requesting /health...' }}</p>
        </div>

        <div class="mt-8 flex gap-3">
          <button class="inline-flex items-center justify-center rounded-md bg-violet-600 px-4 py-2 text-sm font-medium text-white shadow transition hover:bg-violet-500">
            Local connection OK
          </button>
          <button class="inline-flex items-center justify-center rounded-md border border-slate-700 bg-slate-800 px-4 py-2 text-sm font-medium text-slate-200 transition hover:bg-slate-700">
            Axios + env config
          </button>
        </div>
      </div>
    </div>
  </main>
</template>
