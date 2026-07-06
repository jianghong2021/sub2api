<template>
  <div class="min-h-screen bg-gray-50 dark:bg-dark-950">
    <!-- Animated Background -->
    <div class="pointer-events-none fixed inset-0 overflow-hidden">
      <div class="absolute inset-0 bg-[radial-gradient(ellipse_at_top,rgba(139,92,246,0.06),transparent_60%),radial-gradient(ellipse_at_bottom,rgba(124,58,237,0.04),transparent_60%)]"></div>
      <div class="absolute left-1/4 top-1/4 h-[500px] w-[500px] animate-[bgFloat_8s_ease-in-out_infinite] rounded-full bg-gradient-to-br from-primary-500/8 to-primary-700/3 blur-[120px]"></div>
      <div class="absolute bottom-1/4 right-1/4 h-[400px] w-[400px] animate-[bgFloat_10s_ease-in-out_infinite_reverse] rounded-full bg-gradient-to-br from-fuchsia-500/8 to-purple-600/3 blur-[120px]"></div>
      <div
        class="absolute inset-0 opacity-[0.03]"
        style="background-image:
          linear-gradient(rgba(139,92,246,0.3) 1px, transparent 1px),
          linear-gradient(90deg, rgba(139,92,246,0.3) 1px, transparent 1px);
          background-size: 60px 60px;
          mask-image: radial-gradient(ellipse at 50% 30%, black 30%, transparent 70%);
          -webkit-mask-image: radial-gradient(ellipse at 50% 30%, black 30%, transparent 70%);"
      ></div>
      <div class="absolute inset-0 bg-[radial-gradient(ellipse_at_center,transparent_40%,rgba(0,0,0,0.5)_100%)]"></div>
    </div>

    <!-- Sidebar -->
    <AppSidebar />

    <!-- Main Content Area -->
    <div
      class="relative min-h-screen transition-all duration-300"
      :class="[sidebarCollapsed ? 'lg:ml-[72px]' : 'lg:ml-64']"
    >
      <!-- Header -->
      <AppHeader />

      <!-- Main Content -->
      <main class="p-4 md:p-6 lg:p-8">
        <slot />
      </main>
    </div>
  </div>
</template>

<script setup lang="ts">
import '@/styles/onboarding.css'
import { computed, onMounted } from 'vue'
import { useAppStore } from '@/stores'
import { useAuthStore } from '@/stores/auth'
import { useOnboardingTour } from '@/composables/useOnboardingTour'
import { useOnboardingStore } from '@/stores/onboarding'
import AppSidebar from './AppSidebar.vue'
import AppHeader from './AppHeader.vue'

const appStore = useAppStore()
const authStore = useAuthStore()
const sidebarCollapsed = computed(() => appStore.sidebarCollapsed)
const isAdmin = computed(() => authStore.user?.role === 'admin')

const { replayTour } = useOnboardingTour({
  storageKey: isAdmin.value ? 'admin_guide' : 'user_guide',
  autoStart: true
})

const onboardingStore = useOnboardingStore()

onMounted(() => {
  onboardingStore.setReplayCallback(replayTour)
})

defineExpose({ replayTour })
</script>

<style scoped>
@keyframes bgFloat {
  0%, 100% { transform: translate(0, 0) scale(1); }
  25% { transform: translate(40px, -30px) scale(1.05); }
  50% { transform: translate(-20px, 20px) scale(0.95); }
  75% { transform: translate(30px, 40px) scale(1.02); }
}
</style>
