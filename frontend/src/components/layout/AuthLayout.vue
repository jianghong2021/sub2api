<template>
  <div class="relative flex min-h-screen items-center justify-center overflow-hidden bg-dark-950 p-4">
    <!-- Animated Background -->
    <div class="pointer-events-none absolute inset-0 overflow-hidden">
      <div class="absolute inset-0 bg-[radial-gradient(ellipse_at_top,rgba(139,92,246,0.08),transparent_60%),radial-gradient(ellipse_at_bottom,rgba(124,58,237,0.05),transparent_60%)]"></div>
      <div class="absolute -right-40 -top-40 h-80 w-80 animate-[authFloat_8s_ease-in-out_infinite] rounded-full bg-gradient-to-br from-primary-500/15 to-primary-700/8 blur-[100px]"></div>
      <div class="absolute -bottom-40 -left-40 h-80 w-80 animate-[authFloat_10s_ease-in-out_infinite_reverse] rounded-full bg-gradient-to-br from-fuchsia-500/12 to-purple-600/8 blur-[100px]"></div>
      <div class="absolute left-1/2 top-1/2 h-96 w-96 -translate-x-1/2 -translate-y-1/2 animate-[authFloat_12s_ease-in-out_infinite_1s] rounded-full bg-gradient-to-br from-violet-400/10 to-indigo-600/8 blur-[120px]"></div>
      <div class="absolute inset-0 bg-[linear-gradient(rgba(139,92,246,0.04)_1px,transparent_1px),linear-gradient(90deg,rgba(139,92,246,0.04)_1px,transparent_1px)] bg-[size:64px_64px]"></div>
      <div class="absolute inset-0 bg-[radial-gradient(ellipse_at_center,transparent_40%,rgba(0,0,0,0.4)_100%)]"></div>
    </div>

    <!-- Content Container -->
    <div class="relative z-10 w-full max-w-md">
      <!-- Logo/Brand -->
      <div class="mb-8 text-center">
        <template v-if="settingsLoaded">
          <div class="mb-4 inline-flex h-16 w-16 items-center justify-center overflow-hidden rounded-2xl bg-gradient-to-br from-primary-500 to-primary-700 p-0.5 shadow-lg shadow-primary-500/30">
            <div class="flex h-full w-full items-center justify-center rounded-[12px] bg-dark-950">
              <img :src="siteLogo || '/logo.png'" alt="Logo" class="h-11 w-11 object-contain" />
            </div>
          </div>
          <h1 class="mb-2 text-3xl font-bold">
            <span class="bg-gradient-to-r from-white via-white to-primary-200 bg-clip-text text-transparent">{{ siteName }}</span>
          </h1>
          <p class="text-sm text-dark-400">{{ siteSubtitle }}</p>
        </template>
      </div>

      <!-- Card Container -->
      <div class="rounded-2xl border border-white/10 bg-dark-800/50 p-8 shadow-2xl shadow-primary-500/5 backdrop-blur-xl">
        <slot />
      </div>

      <!-- Footer Links -->
      <div class="mt-6 text-center text-sm">
        <slot name="footer" />
      </div>

      <!-- Copyright -->
      <div class="mt-8 text-center text-xs text-dark-500">
        &copy; {{ currentYear }} {{ siteName }}. All rights reserved.
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed, onMounted } from 'vue'
import { useAppStore } from '@/stores'
import { sanitizeUrl } from '@/utils/url'

const appStore = useAppStore()

const siteName = computed(() => appStore.siteName || '大灰狼')
const siteLogo = computed(() => sanitizeUrl(appStore.siteLogo || '', { allowRelative: true, allowDataUrl: true }))
const siteSubtitle = computed(() => appStore.cachedPublicSettings?.site_subtitle || '大灰狼API服务平台')
const settingsLoaded = computed(() => appStore.publicSettingsLoaded)

const currentYear = computed(() => new Date().getFullYear())

onMounted(() => {
  appStore.fetchPublicSettings()
})
</script>

<style scoped>
@keyframes authFloat {
  0%, 100% { transform: translate(0, 0) scale(1); }
  25% { transform: translate(30px, -20px) scale(1.05); }
  50% { transform: translate(-15px, 15px) scale(0.95); }
  75% { transform: translate(20px, 30px) scale(1.02); }
}
</style>
