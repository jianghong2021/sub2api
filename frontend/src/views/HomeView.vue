<template>
  <div v-if="homeContent" class="min-h-screen">
    <iframe
      v-if="isHomeContentUrl"
      :src="homeContent.trim()"
      class="h-screen w-full border-0"
      allowfullscreen
    ></iframe>
    <div v-else v-html="homeContent"></div>
  </div>

  <div v-else class="relative flex min-h-screen flex-col bg-dark-950">
    <!-- ===== Animated Background Layer ===== -->
    <div class="pointer-events-none fixed inset-0 overflow-hidden">
      <div class="absolute inset-0 bg-[radial-gradient(ellipse_at_top,rgba(139,92,246,0.08),transparent_60%),radial-gradient(ellipse_at_bottom,rgba(124,58,237,0.05),transparent_60%)]"></div>
      <!-- Constellation dots -->
      <div class="constellation-dot dot-1"></div><div class="constellation-dot dot-2"></div>
      <div class="constellation-dot dot-3"></div><div class="constellation-dot dot-4"></div>
      <div class="constellation-dot dot-5"></div><div class="constellation-dot dot-6"></div>
      <div class="constellation-dot dot-7"></div><div class="constellation-dot dot-8"></div>
      <div class="constellation-dot dot-9"></div><div class="constellation-dot dot-10"></div>
      <div class="constellation-dot dot-11"></div><div class="constellation-dot dot-12"></div>
      <div class="constellation-line line-1"></div><div class="constellation-line line-2"></div>
      <div class="constellation-line line-3"></div><div class="constellation-line line-4"></div>
      <div class="constellation-line line-5"></div>
      <!-- Floating code fragments -->
      <div class="code-frag frag-1">const API = &lt;Gateway&gt;</div>
      <div class="code-frag frag-2">await proxy.stream()</div>
      <div class="code-frag frag-3">200 OK</div>
      <div class="code-frag frag-4">model: "claude-3"</div>
      <div class="code-frag frag-5">tokens: 4.2k</div>
      <!-- Orbs -->
      <div class="absolute left-1/4 top-1/4 h-[500px] w-[500px] animate-[float_8s_ease-in-out_infinite] rounded-full bg-gradient-to-br from-primary-500/10 to-primary-700/5 blur-[120px]"></div>
      <div class="absolute bottom-1/4 right-1/4 h-[400px] w-[400px] animate-[float_10s_ease-in-out_infinite_reverse] rounded-full bg-gradient-to-br from-fuchsia-500/10 to-purple-600/5 blur-[120px]"></div>
      <div class="absolute left-1/2 top-1/2 h-[300px] w-[300px] -translate-x-1/2 -translate-y-1/2 animate-[float_12s_ease-in-out_infinite_1s] rounded-full bg-gradient-to-br from-violet-400/8 to-indigo-600/5 blur-[100px]"></div>
      <div class="absolute inset-0 opacity-[0.04]" style="background-image:linear-gradient(rgba(139,92,246,0.3) 1px,transparent 1px),linear-gradient(90deg,rgba(139,92,246,0.3) 1px,transparent 1px);background-size:60px 60px;mask-image:radial-gradient(ellipse at 50% 30%,black 30%,transparent 70%);-webkit-mask-image:radial-gradient(ellipse at 50% 30%,black 30%,transparent 70%)"></div>
      <div class="absolute inset-0 bg-[repeating-linear-gradient(0deg,transparent,transparent_2px,rgba(139,92,246,0.015)_2px,rgba(139,92,246,0.015)_4px)]"></div>
      <div class="absolute inset-0 bg-[radial-gradient(ellipse_at_center,transparent_40%,rgba(0,0,0,0.5)_100%)]"></div>
    </div>

    <!-- ===== Sticky Header ===== -->
    <header class="sticky top-0 z-50 border-b border-white/5 bg-dark-950/80 px-6 py-3 backdrop-blur-xl transition-all duration-300" :class="{ 'shadow-lg shadow-primary-500/5': scrolled }">
      <nav class="mx-auto flex max-w-6xl items-center justify-between">
        <div class="flex items-center gap-3">
          <div class="flex h-9 w-9 items-center justify-center overflow-hidden rounded-xl bg-gradient-to-br from-primary-500 to-primary-700 p-0.5 shadow-lg shadow-primary-500/30">
            <div class="flex h-full w-full items-center justify-center rounded-[10px] bg-dark-900">
              <img :src="siteLogo || '/logo.png'" alt="Logo" class="h-6 w-6 object-contain" />
            </div>
          </div>
          <span class="hidden text-sm font-semibold text-white sm:block">{{ siteName }}</span>
        </div>
        <div class="flex items-center gap-1.5">
          <a v-if="docUrl" :href="docUrl" target="_blank" rel="noopener noreferrer" class="rounded-lg p-2 text-dark-400 transition-colors hover:bg-white/5 hover:text-white" :title="t('home.viewDocs')"><Icon name="book" size="md" /></a>
          <router-link v-if="isAuthenticated" :to="dashboardPath" class="inline-flex items-center gap-2 rounded-full bg-gradient-to-r from-primary-500 to-primary-600 px-4 py-1.5 text-xs font-medium text-white shadow-lg shadow-primary-500/30 transition-all hover:shadow-primary-500/50">
            <span class="flex h-5 w-5 items-center justify-center rounded-full bg-white/20 text-[10px] font-semibold text-white">{{ userInitial }}</span>
            <span>{{ t('home.dashboard') }}</span>
          </router-link>
          <router-link v-else to="/login" class="inline-flex items-center rounded-full bg-white/5 px-4 py-1.5 text-xs font-medium text-white ring-1 ring-white/10 transition-all hover:bg-white/10 hover:ring-white/20">{{ t('home.login') }}</router-link>
        </div>
      </nav>
    </header>

    <!-- ===== Main Content ===== -->
    <main class="relative z-10 flex-1">
      <!-- ===== Hero Section ===== -->
      <section class="relative overflow-hidden px-6 pt-24 pb-20 md:pt-32 md:pb-28">
        <!-- Large rotating ring behind hero -->
        <div class="pointer-events-none absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2">
          <div class="hero-ring h-[500px] w-[500px] md:h-[700px] md:w-[700px]"></div>
        </div>

        <div class="mx-auto max-w-6xl">
          <div class="flex flex-col items-center justify-between gap-16 lg:flex-row lg:gap-24">
            <div ref="heroTextRef" class="flex-1 text-center lg:text-left" :class="heroTextVisible ? 'animate-fade-in' : 'opacity-0'">
              <div class="mb-4 inline-flex items-center gap-2 rounded-full border border-primary-500/20 bg-primary-500/10 px-3 py-1 text-xs font-medium text-primary-400">
                <span class="h-1.5 w-1.5 animate-pulse rounded-full bg-primary-400"></span>
                AI API Gateway
              </div>
              <h1 class="glitch-text group relative mb-4 text-4xl font-bold tracking-tight md:text-5xl lg:text-6xl" data-text="siteName">
                <span class="bg-gradient-to-r from-white via-white to-primary-200 bg-clip-text text-transparent">{{ siteName }}</span>
              </h1>
              <p class="mb-10 text-lg text-dark-400 md:text-xl max-w-xl mx-auto lg:mx-0 typewriter">
                {{ siteSubtitle }}
              </p>
              <div class="flex flex-wrap items-center justify-center gap-4 lg:justify-start">
                <router-link :to="isAuthenticated ? dashboardPath : '/login'" class="group relative inline-flex items-center gap-2 overflow-hidden rounded-full bg-gradient-to-r from-primary-500 to-primary-600 px-8 py-3 text-base font-medium text-white shadow-xl shadow-primary-500/30 transition-all hover:shadow-primary-500/50">
                  <span class="absolute inset-0 translate-y-full bg-gradient-to-r from-primary-400 to-primary-500 transition-transform duration-300 group-hover:translate-y-0"></span>
                  <span class="relative z-10">{{ isAuthenticated ? t('home.goToDashboard') : t('home.getStarted') }}</span>
                  <Icon name="arrowRight" size="md" class="relative z-10" :stroke-width="2" />
                </router-link>
                <a v-if="docUrl" :href="docUrl" target="_blank" class="inline-flex items-center gap-2 rounded-full border border-white/10 px-6 py-3 text-sm font-medium text-dark-300 transition-all hover:border-white/20 hover:text-white"><Icon name="book" size="sm" />{{ t('home.viewDocs') }}</a>
              </div>
            </div>

            <div ref="terminalRef" class="flex flex-1 justify-center lg:justify-end" :class="terminalVisible ? 'animate-fade-in' : 'opacity-0'">
              <div class="terminal-container group">
                <div class="terminal-window">
                  <div class="absolute -inset-4 rounded-2xl bg-gradient-to-br from-primary-500/5 via-transparent to-fuchsia-500/5 opacity-0 blur-xl transition-opacity duration-500 group-hover:opacity-100"></div>
                  <div class="terminal-header">
                    <div class="terminal-buttons"><span class="btn-close"></span><span class="btn-minimize"></span><span class="btn-maximize"></span></div>
                    <span class="terminal-title">api-terminal</span>
                    <div class="terminal-status"></div>
                  </div>
                  <div class="terminal-body">
                    <div class="code-line line-1"><span class="code-prompt">$</span><span class="code-cmd">curl</span><span class="code-flag">-X POST</span><span class="code-url">/v1/messages</span></div>
                    <div class="code-line line-2"><span class="code-comment"># Routing to upstream...</span><span class="loading-dots"><span></span><span></span><span></span></span></div>
                    <div class="code-line line-3"><span class="code-success">200 OK</span><span class="code-response">{ "content": "Hello!" }</span></div>
                    <div class="code-line line-4"><span class="code-prompt">$</span><span class="cursor"></span></div>
                    <div class="terminal-progress"><div class="progress-bar-inner"></div></div>
                    <!-- Data stream lines -->
                    <div class="data-stream">latency: 42ms | tokens: 156 | model: claude-sonnet</div>
                    <div class="data-stream data-stream-2">requests/min: 1,247 | avg: 38ms</div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="absolute bottom-0 left-0 right-0 h-px bg-gradient-to-r from-transparent via-primary-500/30 to-transparent"></div>
      </section>

      <!-- ===== Feature Tags + Animated Stats ===== -->
      <section ref="tagsSectionRef" class="px-6 py-16" :class="tagsVisible ? 'animate-slide-up' : 'opacity-0 translate-y-4'">
        <div class="mx-auto max-w-6xl">
          <div class="mb-12 flex flex-wrap items-center justify-center gap-4 md:gap-6">
            <div class="tag-pill group inline-flex items-center gap-2.5 rounded-full border border-primary-500/20 bg-primary-500/5 px-5 py-2.5 backdrop-blur-sm transition-all hover:border-primary-500/30 hover:bg-primary-500/10 hover:shadow-lg hover:shadow-primary-500/5">
              <Icon name="bolt" size="sm" class="text-primary-400" /><span class="text-sm font-medium text-dark-200">{{ t('home.tags.subscriptionToApi') }}</span>
            </div>
            <div class="tag-pill group inline-flex items-center gap-2.5 rounded-full border border-primary-500/20 bg-primary-500/5 px-5 py-2.5 backdrop-blur-sm transition-all hover:border-primary-500/30 hover:bg-primary-500/10 hover:shadow-lg hover:shadow-primary-500/5">
              <Icon name="shield" size="sm" class="text-primary-400" /><span class="text-sm font-medium text-dark-200">{{ t('home.tags.stickySession') }}</span>
            </div>
            <div class="tag-pill group inline-flex items-center gap-2.5 rounded-full border border-primary-500/20 bg-primary-500/5 px-5 py-2.5 backdrop-blur-sm transition-all hover:border-primary-500/30 hover:bg-primary-500/10 hover:shadow-lg hover:shadow-primary-500/5">
              <Icon name="chart" size="sm" class="text-primary-400" /><span class="text-sm font-medium text-dark-200">{{ t('home.tags.realtimeBilling') }}</span>
            </div>
          </div>

          <!-- Animated Stats Row -->
          <div class="grid gap-4 sm:grid-cols-3">
            <div class="stat-glow group relative overflow-hidden rounded-xl border border-white/5 bg-dark-800/30 px-6 py-5 text-center backdrop-blur-sm">
              <div class="absolute inset-0 bg-gradient-to-b from-primary-500/0 via-primary-500/0 to-primary-500/5 opacity-0 transition-opacity duration-500 group-hover:opacity-100"></div>
              <div class="relative text-2xl font-bold tracking-wider text-white"><span class="stat-value" data-target="99.9">0</span>%</div>
              <div class="relative mt-1 text-xs text-dark-400">Uptime SLA</div>
            </div>
            <div class="stat-glow group relative overflow-hidden rounded-xl border border-white/5 bg-dark-800/30 px-6 py-5 text-center backdrop-blur-sm">
              <div class="absolute inset-0 bg-gradient-to-b from-primary-500/0 via-primary-500/0 to-primary-500/5 opacity-0 transition-opacity duration-500 group-hover:opacity-100"></div>
              <div class="relative text-2xl font-bold tracking-wider text-white"><span class="stat-value" data-target="50">0</span>ms</div>
              <div class="relative mt-1 text-xs text-dark-400">Avg. Latency</div>
            </div>
            <div class="stat-glow group relative overflow-hidden rounded-xl border border-white/5 bg-dark-800/30 px-6 py-5 text-center backdrop-blur-sm">
              <div class="absolute inset-0 bg-gradient-to-b from-primary-500/0 via-primary-500/0 to-primary-500/5 opacity-0 transition-opacity duration-500 group-hover:opacity-100"></div>
              <div class="relative text-2xl font-bold bg-gradient-to-r from-primary-400 to-primary-200 bg-clip-text text-transparent">∞</div>
              <div class="relative mt-1 text-xs text-dark-400">Auto Scaling</div>
            </div>
          </div>
        </div>
      </section>

      <!-- ===== Features Grid ===== -->
      <section ref="featuresRef" class="relative px-6 py-20">
        <div class="absolute inset-0 bg-[radial-gradient(ellipse_at_center,rgba(139,92,246,0.03),transparent_60%)] pointer-events-none"></div>
        <div class="mx-auto max-w-6xl">
          <div class="mb-12 text-center">
            <h2 class="text-3xl font-bold text-white md:text-4xl"><span class="bg-gradient-to-r from-white to-primary-200 bg-clip-text text-transparent">Core Features</span></h2>
            <p class="mt-3 text-dark-400">Everything you need to manage AI API access</p>
          </div>
          <div class="grid gap-6 md:grid-cols-3">
            <div v-for="(feature, idx) in features" :key="idx" ref="featureCardRefs" class="feature-card group relative overflow-hidden rounded-2xl p-7 transition-all duration-500" :class="featureCardsVisible[idx] ? 'animate-slide-up' : 'opacity-0 translate-y-6'" :style="{ animationDelay: `${idx * 0.1}s` }">
              <!-- Animated gradient border -->
              <div class="card-border-gradient"></div>
              <div class="absolute -right-8 -top-8 h-24 w-24 rounded-full bg-primary-500/5 blur-2xl transition-all duration-500 group-hover:bg-primary-500/15 group-hover:blur-3xl"></div>
              <div class="relative mb-5 flex h-13 w-13 items-center justify-center rounded-xl transition-transform duration-300 group-hover:scale-110 group-hover:-translate-y-1" :class="feature.iconBg">
                <Icon v-if="idx === 0" name="server" size="lg" class="text-blue-400" />
                <svg v-else class="h-6 w-6" :class="feature.iconColor" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5" v-html="feature.iconPath"></svg>
              </div>
              <h3 class="relative mb-3 text-lg font-semibold text-white">{{ feature.title }}</h3>
              <p class="relative text-sm leading-relaxed text-dark-400">{{ feature.desc }}</p>
              <div class="relative mt-4 flex items-center gap-1 text-xs font-medium text-primary-400 opacity-0 transition-all duration-300 group-hover:opacity-100 group-hover:translate-x-0 -translate-x-2">
                <span>Learn more</span>
                <svg class="h-3 w-3" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M8.25 4.5l7.5 7.5-7.5 7.5"/></svg>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- ===== Supported Providers ===== -->
      <section ref="providersRef" class="relative px-6 py-20" :class="providersVisible ? 'animate-fade-in' : 'opacity-0'">
        <div class="absolute inset-0 bg-gradient-to-b from-transparent via-primary-500/[0.02] to-transparent pointer-events-none"></div>
        <div class="mx-auto max-w-6xl">
          <div class="mb-10 text-center">
            <h2 class="mb-3 text-3xl font-bold text-white md:text-4xl"><span class="bg-gradient-to-r from-white to-primary-200 bg-clip-text text-transparent">{{ t('home.providers.title') }}</span></h2>
            <p class="text-dark-400">{{ t('home.providers.description') }}</p>
          </div>
          <div class="flex flex-wrap items-center justify-center gap-4">
            <div v-for="(provider, idx) in providers" :key="idx" class="flex items-center gap-2 rounded-xl border px-5 py-3 backdrop-blur-sm transition-all duration-300" :class="provider.active ? 'border-primary-500/20 bg-primary-500/5 ring-1 ring-primary-500/20 hover:border-primary-500/30 hover:bg-primary-500/10 hover:ring-primary-500/30 hover:-translate-y-0.5' : 'border-white/5 bg-dark-800/20 opacity-60 hover:opacity-80'">
              <div class="flex h-8 w-8 items-center justify-center rounded-lg shadow-lg" :class="provider.badge"><span class="text-xs font-bold text-white">{{ provider.initial }}</span></div>
              <span class="text-sm font-medium" :class="provider.active ? 'text-dark-200' : 'text-dark-300'">{{ provider.name }}</span>
              <span class="rounded px-1.5 py-0.5 text-[10px] font-medium" :class="provider.active ? 'bg-primary-500/20 text-primary-400' : 'bg-dark-700 text-dark-400'">{{ provider.active ? t('home.providers.supported') : t('home.providers.soon') }}</span>
            </div>
          </div>
        </div>
      </section>
    </main>

    <!-- Footer -->
    <footer class="relative z-10 border-t border-white/5 px-6 py-10">
      <div class="mx-auto flex max-w-6xl flex-col items-center justify-between gap-6 text-center sm:flex-row sm:text-left">
        <div class="flex items-center gap-3">
          <div class="flex h-7 w-7 items-center justify-center rounded-lg bg-gradient-to-br from-primary-500 to-primary-700 p-0.5"><div class="flex h-full w-full items-center justify-center rounded-md bg-dark-900"><img :src="siteLogo || '/logo.png'" alt="" class="h-4 w-4 object-contain" /></div></div>
          <span class="text-xs text-dark-500">&copy; {{ currentYear }} {{ siteName }}. {{ t('home.footer.allRightsReserved') }}</span>
        </div>
        <div class="flex items-center gap-6">
          <a v-if="docUrl" :href="docUrl" target="_blank" rel="noopener noreferrer" class="text-xs text-dark-500 transition-colors hover:text-white">{{ t('home.docs') }}</a>
        </div>
      </div>
    </footer>
  </div>
</template>

<script setup lang="ts">
import { ref, computed, onMounted, watchEffect } from 'vue'
import { useI18n } from 'vue-i18n'
import { useAuthStore, useAppStore } from '@/stores'
import Icon from '@/components/icons/Icon.vue'

const { t } = useI18n()
const authStore = useAuthStore()
const appStore = useAppStore()

const siteName = computed(() => appStore.cachedPublicSettings?.site_name || appStore.siteName || '大灰狼')
const siteLogo = computed(() => appStore.cachedPublicSettings?.site_logo || appStore.siteLogo || '')
const siteSubtitle = computed(() => appStore.cachedPublicSettings?.site_subtitle || 'AI API Gateway Platform')
const docUrl = computed(() => appStore.cachedPublicSettings?.doc_url || appStore.docUrl || '')
const homeContent = computed(() => appStore.cachedPublicSettings?.home_content || '')

const isHomeContentUrl = computed(() => {
  const content = homeContent.value.trim()
  return content.startsWith('http://') || content.startsWith('https://')
})

const isAuthenticated = computed(() => authStore.isAuthenticated)
const isAdmin = computed(() => authStore.isAdmin)
const dashboardPath = computed(() => isAdmin.value ? '/admin/dashboard' : '/dashboard')
const userInitial = computed(() => {
  const user = authStore.user
  if (!user || !user.email) return ''
  return user.email.charAt(0).toUpperCase()
})
const currentYear = computed(() => new Date().getFullYear())

const scrolled = ref(false)
const heroTextRef = ref<HTMLElement | null>(null)
const terminalRef = ref<HTMLElement | null>(null)
const tagsSectionRef = ref<HTMLElement | null>(null)
const featuresRef = ref<HTMLElement | null>(null)
const providersRef = ref<HTMLElement | null>(null)
const heroTextVisible = ref(false)
const terminalVisible = ref(false)
const tagsVisible = ref(false)
const providersVisible = ref(false)
const featureCardRefs = ref<(HTMLElement | null)[]>([])
const featureCardsVisible = ref<boolean[]>([])

const features = computed(() => [
  { title: t('home.features.unifiedGateway'), desc: t('home.features.unifiedGatewayDesc'), iconBg: 'bg-gradient-to-br from-blue-500/20 to-blue-600/20 ring-1 ring-blue-500/30 group-hover:ring-blue-500/50', iconColor: 'text-blue-400', iconPath: '' },
  { title: t('home.features.multiAccount'), desc: t('home.features.multiAccountDesc'), iconBg: 'bg-gradient-to-br from-primary-500/20 to-primary-600/20 ring-1 ring-primary-500/30 group-hover:ring-primary-500/50', iconColor: 'text-primary-400', iconPath: '<path stroke-linecap="round" stroke-linejoin="round" d="M18 18.72a9.094 9.094 0 003.741-.479 3 3 0 00-4.682-2.72m.94 3.198l.001.031c0 .225-.012.447-.037.666A11.944 11.944 0 0112 21c-2.17 0-4.207-.576-5.963-1.584A6.062 6.062 0 016 18.719m12 0a5.971 5.971 0 00-.941-3.197m0 0A5.995 5.995 0 0012 12.75a5.995 5.995 0 00-5.058 2.772m0 0a3 3 0 00-4.681 2.72 8.986 8.986 0 003.74.477m.94-3.197a5.971 5.971 0 00-.94 3.197M15 6.75a3 3 0 11-6 0 3 3 0 016 0zm6 3a2.25 2.25 0 11-4.5 0 2.25 2.25 0 014.5 0zm-13.5 0a2.25 2.25 0 11-4.5 0 2.25 2.25 0 014.5 0z" />' },
  { title: t('home.features.balanceQuota'), desc: t('home.features.balanceQuotaDesc'), iconBg: 'bg-gradient-to-br from-purple-500/20 to-purple-600/20 ring-1 ring-purple-500/30 group-hover:ring-purple-500/50', iconColor: 'text-purple-400', iconPath: '<path stroke-linecap="round" stroke-linejoin="round" d="M2.25 18.75a60.07 60.07 0 0115.797 2.101c.727.198 1.453-.342 1.453-1.096V18.75M3.75 4.5v.75A.75.75 0 013 6h-.75m0 0v-.375c0-.621.504-1.125 1.125-1.125H20.25M2.25 6v9m18-10.5v.75c0 .414.336.75.75.75h.75m-1.5-1.5h.375c.621 0 1.125.504 1.125 1.125v9.75c0 .621-.504 1.125-1.125 1.125h-.375m1.5-1.5H21a.75.75 0 00-.75.75v.75m0 0H3.75m0 0h-.375a1.125 1.125 0 01-1.125-1.125V15m1.5 1.5v-.75A.75.75 0 003 15h-.75M15 10.5a3 3 0 11-6 0 3 3 0 016 0zm3 0h.008v.008H18V10.5zm-12 0h.008v.008H6V10.5z" />' }
])

const providers = computed(() => [
  { name: t('home.providers.claude'), initial: 'C', badge: 'bg-gradient-to-br from-orange-500 to-orange-600 shadow-orange-500/20', active: true },
  { name: 'GPT', initial: 'G', badge: 'bg-gradient-to-br from-green-500 to-green-600 shadow-green-500/20', active: true },
  { name: t('home.providers.gemini'), initial: 'G', badge: 'bg-gradient-to-br from-blue-500 to-blue-600 shadow-blue-500/20', active: true },
  { name: t('home.providers.antigravity'), initial: 'A', badge: 'bg-gradient-to-br from-rose-500 to-pink-600 shadow-rose-500/20', active: true },
  { name: t('home.providers.more'), initial: '+', badge: 'bg-gradient-to-br from-dark-600 to-dark-500', active: false }
])

function initTheme() {
  const savedTheme = localStorage.getItem('theme')
  if (savedTheme === 'dark' || (!savedTheme && window.matchMedia('(prefers-color-scheme: dark)').matches)) {
    document.documentElement.classList.add('dark')
  }
}

function observeElement(el: HTMLElement | null, callback: (v: boolean) => void) {
  if (!el) return
  const observer = new IntersectionObserver(([entry]) => { if (entry.isIntersecting) { callback(true); observer.disconnect() } }, { threshold: 0.15 })
  observer.observe(el)
}

function animateCounter(el: HTMLElement) {
  const target = parseFloat(el.dataset.target || '0')
  const duration = 2000
  const startTime = performance.now()
  const isDecimal = target % 1 !== 0

  function update(currentTime: number) {
    const elapsed = currentTime - startTime
    const progress = Math.min(elapsed / duration, 1)
    const eased = 1 - Math.pow(1 - progress, 3)
    const current = target * eased
    el.textContent = isDecimal ? current.toFixed(1) : Math.floor(current).toString()
    if (progress < 1) requestAnimationFrame(update)
  }
  requestAnimationFrame(update)
}

onMounted(() => {
  initTheme()
  authStore.checkAuth()
  if (!appStore.publicSettingsLoaded) appStore.fetchPublicSettings()

  const handleScroll = () => { scrolled.value = window.scrollY > 20 }
  window.addEventListener('scroll', handleScroll, { passive: true })

  observeElement(heroTextRef.value, (v) => { heroTextVisible.value = v })
  observeElement(terminalRef.value, (v) => { terminalVisible.value = v })
  observeElement(tagsSectionRef.value, (v) => { tagsVisible.value = v })
  observeElement(providersRef.value, (v) => { providersVisible.value = v })

  const fObserver = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        const idx = featureCardRefs.value.indexOf(entry.target as HTMLElement)
        if (idx !== -1) { featureCardsVisible.value[idx] = true }
        fObserver.unobserve(entry.target)
      }
    })
  }, { threshold: 0.2 })
  featureCardRefs.value.forEach((el) => { if (el) fObserver.observe(el) })

  // Animate counters when tags section is visible
  watchEffect(() => {
    if (tagsVisible.value) {
      setTimeout(() => {
        document.querySelectorAll('.stat-value').forEach((el) => animateCounter(el as HTMLElement))
      }, 400)
    }
  })
})
</script>

<style scoped>
/* ===== Floating Orbs ===== */
@keyframes float {
  0%, 100% { transform: translate(0, 0) scale(1); }
  25% { transform: translate(40px, -30px) scale(1.05); }
  50% { transform: translate(-20px, 20px) scale(0.95); }
  75% { transform: translate(30px, 40px) scale(1.02); }
}

/* ===== Hero Rotating Ring ===== */
.hero-ring {
  position: relative;
  border: 1px solid rgba(139, 92, 246, 0.08);
  border-radius: 50%;
  animation: ring-rotate 30s linear infinite;
}

.hero-ring::before {
  content: '';
  position: absolute;
  inset: -1px;
  border-radius: 50%;
  background: conic-gradient(from 0deg, transparent, rgba(139, 92, 246, 0.15), transparent 30%, rgba(139, 92, 246, 0.08) 50%, transparent 70%, rgba(167, 139, 250, 0.12) 85%, transparent);
  -webkit-mask: radial-gradient(farthest-side, transparent calc(100% - 1px), #000 calc(100% - 1px));
  mask: radial-gradient(farthest-side, transparent calc(100% - 1px), #000 calc(100% - 1px));
  animation: ring-glow 4s ease-in-out infinite alternate;
}

.hero-ring::after {
  content: '';
  position: absolute;
  top: 50%;
  left: 50%;
  width: 60%;
  height: 60%;
  transform: translate(-50%, -50%);
  border: 1px solid rgba(139, 92, 246, 0.06);
  border-radius: 50%;
  animation: ring-rotate 20s linear infinite reverse;
}

@keyframes ring-rotate {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}

@keyframes ring-glow {
  0% { opacity: 0.5; }
  100% { opacity: 1; }
}

/* ===== Glitch Text ===== */
.glitch-text {
  position: relative;
}

/* ===== Typewriter Effect ===== */
.typewriter {
  overflow: hidden;
  white-space: nowrap;
  border-right: 2px solid rgba(139, 92, 246, 0.6);
  animation: typewriter 2.5s steps(30) 0.5s forwards, blink-caret 0.8s step-end infinite;
  max-width: fit-content;
}

@keyframes typewriter {
  from { width: 0; }
  to { width: 100%; }
}

@keyframes blink-caret {
  0%, 100% { border-color: rgba(139, 92, 246, 0.6); }
  50% { border-color: transparent; }
}

/* ===== Constellation Dots ===== */
.constellation-dot {
  position: absolute;
  width: 3px;
  height: 3px;
  border-radius: 50%;
  background: rgba(139, 92, 246, 0.5);
  box-shadow: 0 0 6px rgba(139, 92, 246, 0.3);
  animation: twinkle 3s ease-in-out infinite;
}

.dot-1 { left: 15%; top: 25%; animation-delay: 0s; }
.dot-2 { left: 22%; top: 20%; animation-delay: 0.4s; }
.dot-3 { left: 28%; top: 30%; animation-delay: 0.8s; }
.dot-4 { left: 70%; top: 35%; animation-delay: 0.2s; }
.dot-5 { left: 78%; top: 28%; animation-delay: 0.6s; }
.dot-6 { left: 85%; top: 40%; animation-delay: 1s; }
.dot-7 { left: 45%; top: 65%; animation-delay: 0.3s; }
.dot-8 { left: 52%; top: 70%; animation-delay: 0.7s; }
.dot-9 { left: 60%; top: 60%; animation-delay: 1.1s; }
.dot-10 { left: 35%; top: 75%; animation-delay: 0.5s; }
.dot-11 { left: 40%; top: 68%; animation-delay: 0.9s; }
.dot-12 { left: 50%; top: 55%; animation-delay: 0.1s; }

@keyframes twinkle {
  0%, 100% { opacity: 0.3; transform: scale(1); }
  50% { opacity: 1; transform: scale(1.5); }
}

/* Constellation connecting lines using pseudo-elements */
.constellation-line {
  position: absolute;
  height: 1px;
  background: linear-gradient(90deg, rgba(139, 92, 246, 0.15), transparent);
  animation: line-pulse 4s ease-in-out infinite;
}

.line-1 { left: 15%; top: 25%; width: 80px; transform: rotate(30deg); transform-origin: left center; animation-delay: 0s; }
.line-2 { left: 22%; top: 20%; width: 60px; transform: rotate(-20deg); transform-origin: left center; animation-delay: 0.5s; }
.line-3 { left: 70%; top: 35%; width: 90px; transform: rotate(-15deg); transform-origin: left center; animation-delay: 1s; }
.line-4 { left: 45%; top: 65%; width: 70px; transform: rotate(25deg); transform-origin: left center; animation-delay: 1.5s; }
.line-5 { left: 35%; top: 75%; width: 100px; transform: rotate(-10deg); transform-origin: left center; animation-delay: 2s; }

@keyframes line-pulse {
  0%, 100% { opacity: 0.3; }
  50% { opacity: 1; }
}

/* ===== Floating Code Fragments ===== */
.code-frag {
  position: absolute;
  font-family: ui-monospace, monospace;
  font-size: 11px;
  color: rgba(139, 92, 246, 0.15);
  white-space: nowrap;
  pointer-events: none;
  animation: frag-float linear infinite;
  opacity: 0;
}

.frag-1 { left: 8%; top: 40%; animation-duration: 20s; animation-delay: 0s; }
.frag-2 { left: 75%; top: 55%; animation-duration: 22s; animation-delay: 3s; }
.frag-3 { left: 5%; top: 70%; animation-duration: 18s; animation-delay: 6s; }
.frag-4 { left: 82%; top: 20%; animation-duration: 25s; animation-delay: 2s; }
.frag-5 { left: 50%; top: 80%; animation-duration: 20s; animation-delay: 8s; }

@keyframes frag-float {
  0% { transform: translateY(0) translateX(0); opacity: 0; }
  10% { opacity: 0.4; }
  90% { opacity: 0.4; }
  100% { transform: translateY(-200px) translateX(30px); opacity: 0; }
}

/* ===== Terminal ===== */
.terminal-container { position: relative; display: inline-block; }

.terminal-window {
  position: relative;
  width: 440px;
  background: linear-gradient(145deg, rgba(30, 41, 59, 0.92) 0%, rgba(15, 23, 42, 0.96) 100%);
  border-radius: 14px;
  box-shadow: 0 25px 60px -12px rgba(0, 0, 0, 0.5), 0 0 0 1px rgba(139, 92, 246, 0.15), 0 0 30px rgba(139, 92, 246, 0.05), inset 0 1px 0 rgba(255, 255, 255, 0.05);
  overflow: hidden;
  transform: perspective(1000px) rotateX(2deg) rotateY(-2deg);
  transition: transform 0.4s cubic-bezier(0.34, 1.56, 0.64, 1), box-shadow 0.4s ease;
}

.terminal-window:hover {
  transform: perspective(1000px) rotateX(0deg) rotateY(0deg) translateY(-6px);
  box-shadow: 0 35px 80px -12px rgba(0, 0, 0, 0.6), 0 0 0 1px rgba(139, 92, 246, 0.25), 0 0 50px rgba(139, 92, 246, 0.1), inset 0 1px 0 rgba(255, 255, 255, 0.05);
}

.terminal-header {
  display: flex;
  align-items: center;
  padding: 12px 16px;
  background: rgba(30, 41, 59, 0.5);
  border-bottom: 1px solid rgba(255, 255, 255, 0.05);
}

.terminal-buttons { display: flex; gap: 8px; }
.terminal-buttons span { width: 12px; height: 12px; border-radius: 50%; transition: filter 0.2s; }
.terminal-buttons span:hover { filter: brightness(1.3); }
.btn-close { background: #ef4444; }
.btn-minimize { background: #eab308; }
.btn-maximize { background: #22c55e; }

.terminal-title { flex: 1; text-align: center; font-size: 12px; font-family: ui-monospace, monospace; color: #64748b; margin-right: 52px; }
.terminal-status { width: 6px; height: 6px; border-radius: 50%; background: #22c55e; box-shadow: 0 0 6px rgba(34, 197, 94, 0.5); }

.terminal-body { padding: 20px 24px; font-family: ui-monospace, 'Fira Code', monospace; font-size: 14px; line-height: 2; }

.code-line { display: flex; align-items: center; gap: 8px; flex-wrap: wrap; opacity: 0; animation: line-appear 0.5s ease forwards; }
.line-1 { animation-delay: 0.3s; }
.line-2 { animation-delay: 1s; }
.line-3 { animation-delay: 1.8s; }
.line-4 { animation-delay: 2.5s; }

@keyframes line-appear { from { opacity: 0; transform: translateY(5px); } to { opacity: 1; transform: translateY(0); } }

.code-prompt { color: #22c55e; font-weight: bold; }
.code-cmd { color: #38bdf8; }
.code-flag { color: #a78bfa; }
.code-url { color: #8b5cf6; }
.code-comment { color: #64748b; font-style: italic; }
.code-success { color: #22c55e; background: rgba(34, 197, 94, 0.15); padding: 2px 8px; border-radius: 4px; font-weight: 600; }
.code-response { color: #fbbf24; }

/* Loading dots */
.loading-dots { display: inline-flex; gap: 3px; }
.loading-dots span { width: 4px; height: 4px; border-radius: 50%; background: #64748b; animation: dot-bounce 1.4s ease-in-out infinite; }
.loading-dots span:nth-child(1) { animation-delay: 0s; }
.loading-dots span:nth-child(2) { animation-delay: 0.2s; }
.loading-dots span:nth-child(3) { animation-delay: 0.4s; }

@keyframes dot-bounce { 0%, 80%, 100% { transform: translateY(0); opacity: 0.4; } 40% { transform: translateY(-4px); opacity: 1; } }

.cursor { display: inline-block; width: 8px; height: 16px; background: #8b5cf6; box-shadow: 0 0 6px rgba(139, 92, 246, 0.5); animation: blink 1s step-end infinite; }
@keyframes blink { 0%, 50% { opacity: 1; } 51%, 100% { opacity: 0; } }

.terminal-progress { margin-top: 16px; height: 2px; background: rgba(255, 255, 255, 0.05); border-radius: 1px; overflow: hidden; }
.progress-bar-inner { height: 100%; width: 0%; background: linear-gradient(90deg, transparent, #8b5cf6, #a78bfa, transparent); background-size: 200% 100%; animation: progress-scan 3s ease-in-out infinite, shimmer 2s linear infinite; }
@keyframes progress-scan { 0% { width: 0%; } 50% { width: 100%; } 100% { width: 0%; } }
@keyframes shimmer { 0% { background-position: 200% 0; } 100% { background-position: -200% 0; } }

/* Data stream in terminal */
.data-stream {
  margin-top: 8px;
  font-size: 11px;
  color: rgba(139, 92, 246, 0.3);
  opacity: 0;
  animation: stream-fade 6s ease-in-out infinite;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.data-stream-2 {
  animation-delay: 3s;
  color: rgba(167, 139, 250, 0.2);
}

@keyframes stream-fade {
  0%, 100% { opacity: 0; transform: translateX(-10px); }
  20%, 80% { opacity: 1; transform: translateX(0); }
}

/* ===== Feature Cards with Animated Gradient Border ===== */
.feature-card {
  background: rgba(15, 23, 42, 0.4);
  border: 1px solid rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(4px);
}

.feature-card::before {
  content: '';
  position: absolute;
  inset: -1px;
  border-radius: inherit;
  padding: 1px;
  background: conic-gradient(from 0deg, transparent, transparent, transparent, transparent);
  -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
  -webkit-mask-composite: xor;
  mask-composite: exclude;
  transition: all 0.6s ease;
  pointer-events: none;
}

.feature-card:hover::before {
  background: conic-gradient(from 0deg, transparent, rgba(139, 92, 246, 0.4), rgba(167, 139, 250, 0.3), rgba(139, 92, 246, 0.4), transparent 60%, transparent);
  animation: border-spin 2s linear infinite;
}

@keyframes border-spin {
  to { transform: rotate(360deg); }
}

.feature-card:hover {
  border-color: transparent;
  box-shadow: 0 20px 60px -12px rgba(139, 92, 246, 0.15);
}

/* ===== Stat Glow ===== */
.stat-glow:hover {
  border-color: rgba(139, 92, 246, 0.3);
}

.stat-glow .text-2xl {
  transition: text-shadow 0.3s;
}

.stat-glow:hover .text-2xl {
  text-shadow: 0 0 20px rgba(139, 92, 246, 0.3), 0 0 40px rgba(139, 92, 246, 0.1);
}

/* ===== Tag Pill ===== */
.tag-pill {
  position: relative;
}

/* ===== Keep card height equal ===== */
:deep(.h-13) { height: 3.25rem; }
:deep(.w-13) { width: 3.25rem; }

/* ===== Light mode overrides ===== */
:global(.light) .terminal-window { background: linear-gradient(145deg, #f8fafc 0%, #f1f5f9 100%); box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.15), 0 0 0 1px rgba(0, 0, 0, 0.06), inset 0 1px 0 rgba(255, 255, 255, 0.8); }
:global(.light) .terminal-header { background: rgba(241, 245, 249, 0.8); border-bottom: 1px solid rgba(0, 0, 0, 0.05); }
:global(.light) .terminal-title { color: #94a3b8; }
:global(.light) .code-prompt { color: #16a34a; }
:global(.light) .code-cmd { color: #2563eb; }
:global(.light) .code-flag { color: #7c3aed; }
:global(.light) .code-url { color: #6d28d9; }
:global(.light) .code-comment { color: #94a3b8; }
:global(.light) .code-success { color: #16a34a; background: rgba(22, 163, 74, 0.1); }
:global(.light) .code-response { color: #d97706; }
:global(.light) .cursor { background: #7c3aed; box-shadow: none; }
:global(.light) .terminal-progress { background: rgba(0, 0, 0, 0.05); }
</style>
