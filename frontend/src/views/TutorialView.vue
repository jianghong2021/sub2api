<template>
  <div class="min-h-screen bg-gray-50 dark:bg-dark-950">
    <!-- Header -->
    <header class="sticky top-0 z-50 border-b border-gray-200 bg-white/80 px-6 py-3 backdrop-blur-xl dark:border-white/5 dark:bg-dark-950/80">
      <nav class="mx-auto flex max-w-4xl items-center justify-between">
        <router-link to="/home" class="flex items-center gap-3">
          <div class="flex h-9 w-9 items-center justify-center overflow-hidden rounded-xl bg-gradient-to-br from-primary-500 to-primary-700 p-0.5 shadow-lg shadow-primary-500/30">
            <div class="flex h-full w-full items-center justify-center rounded-[10px] bg-white dark:bg-dark-900">
              <img :src="siteLogo || '/logo.png'" alt="Logo" class="h-6 w-6 object-contain" />
            </div>
          </div>
          <span class="hidden text-sm font-semibold text-gray-900 sm:block dark:text-white">{{ siteName }}</span>
        </router-link>
        <div class="flex items-center gap-3">
          <router-link to="/home" class="text-sm text-gray-500 hover:text-gray-900 dark:text-dark-400 dark:hover:text-white">首页</router-link>
          <span class="text-gray-300 dark:text-dark-600">|</span>
          <span class="text-sm font-medium text-primary-600 dark:text-primary-400">使用教程</span>
        </div>
      </nav>
    </header>

    <!-- Content -->
    <main class="mx-auto max-w-4xl px-6 py-12">
      <h1 class="mb-2 text-3xl font-bold text-gray-900 dark:text-white">使用教程</h1>
      <p class="mb-10 text-gray-500 dark:text-dark-400">快速上手 {{ siteName }}，只需简单两步</p>

      <!-- Step 1 -->
      <div class="mb-8 overflow-hidden rounded-2xl border border-gray-200 bg-white shadow-sm dark:border-white/5 dark:bg-dark-900/50">
        <div class="flex items-center gap-4 border-b border-gray-100 bg-gradient-to-r from-primary-500/5 to-primary-500/10 px-6 py-4 dark:border-white/5">
          <span class="flex h-8 w-8 items-center justify-center rounded-full bg-primary-500 text-sm font-bold text-white">1</span>
          <h2 class="text-lg font-semibold text-gray-900 dark:text-white">购买卡密，兑换金额</h2>
        </div>
        <div class="px-6 py-5">
          <ol class="ml-6 list-decimal space-y-3 text-gray-600 dark:text-dark-300">
            <li>联系客服购买卡密（卡密是一串兑换码）。</li>
            <li>登录后进入 <router-link to="/redeem" class="font-medium text-primary-500 hover:text-primary-600">兑换页面</router-link>，输入卡密点击兑换，金额将自动充入您的账户余额。</li>
            <li>在 <strong class=" text-purple-600">获取兑换码</strong>  页面选择套餐并使用余额支付，即可开通 API 访问权限。</li>
          </ol>
        </div>
      </div>

      <!-- Step 2 -->
      <div class="overflow-hidden rounded-2xl border border-gray-200 bg-white shadow-sm dark:border-white/5 dark:bg-dark-900/50">
        <div class="flex items-center gap-4 border-b border-gray-100 bg-gradient-to-r from-primary-500/5 to-primary-500/10 px-6 py-4 dark:border-white/5">
          <span class="flex h-8 w-8 items-center justify-center rounded-full bg-primary-500 text-sm font-bold text-white">2</span>
          <h2 class="text-lg font-semibold text-gray-900 dark:text-white">创建 API 密钥，配置 OpenCode</h2>
        </div>
        <div class="px-6 py-5 space-y-5">
          <p class="text-gray-600 dark:text-dark-300">登录后进入 <router-link to="/keys" class="font-medium text-primary-500 hover:text-primary-600">API 密钥管理</router-link> 页面，创建一个新的 API 密钥，然后按以下步骤配置 OpenCode：</p>

          <div class="rounded-xl border border-gray-200 bg-gray-50/50 p-5 dark:border-white/5 dark:bg-dark-800/30">
            <h3 class="mb-3 flex items-center gap-2 text-base font-semibold text-gray-900 dark:text-white">
              <span class="flex h-6 w-6 items-center justify-center rounded-md bg-primary-500/10 text-xs font-bold text-primary-500">i</span>
              在 OpenCode 中配置
            </h3>
            <ol class="ml-6 list-decimal space-y-2.5 text-sm text-gray-600 dark:text-dark-300">
              <li>在 OpenCode 终端中输入 <code class="rounded-md bg-gray-200 px-2 py-0.5 font-mono text-xs text-gray-800 dark:bg-dark-700 dark:text-dark-200">/connect</code> 并按回车。</li>
              <li>选择 <code class="rounded-md bg-gray-200 px-2 py-0.5 font-mono text-xs text-gray-800 dark:bg-dark-700 dark:text-dark-200">Other provider</code>。</li>
              <li>输入 <code class="rounded-md bg-gray-200 px-2 py-0.5 font-mono text-xs font-semibold text-gray-800 dark:bg-dark-700 dark:text-dark-200">dahuilang</code> 作为 provider 名称。</li>
              <li>输入您创建的 API 密钥。</li>
              <li>复制生成的配置内容。</li>
              <li>打开用户文件夹下的 <code class="rounded-md bg-gray-200 px-2 py-0.5 font-mono text-xs text-gray-800 dark:bg-dark-700 dark:text-dark-200">~/.config/opencode/opencode.jsonc</code>，粘贴覆盖保存。</li>
              <li>重新打开 OpenCode，即可开始使用。</li>
            </ol>
          </div>

          <div class="rounded-xl border border-amber-200 bg-amber-50 p-4 dark:border-amber-500/20 dark:bg-amber-500/5">
            <p class="flex items-start gap-2 text-sm text-amber-800 dark:text-amber-300">
              <span class="flex h-5 w-5 flex-shrink-0 items-center justify-center rounded-full bg-amber-200 text-xs font-bold text-amber-800 dark:bg-amber-500/20 dark:text-amber-300">!</span>
              配置文件的完整路径：<code class="rounded bg-amber-100 px-1.5 py-0.5 font-mono text-xs dark:bg-amber-500/10">用户/.config/opencode/opencode.jsonc</code>。保存后重启 OpenCode 即可生效。
            </p>
          </div>
        </div>
      </div>

      <!-- Help -->
      <div class="mt-10 text-center">
        <p class="text-sm text-gray-400 dark:text-dark-500">遇到问题？请联系客服获取帮助</p>
      </div>
    </main>

    <!-- Footer -->
    <footer class="border-t border-gray-200 px-6 py-8 dark:border-white/5">
      <div class="mx-auto flex max-w-4xl flex-col items-center justify-between gap-4 text-center sm:flex-row sm:text-left">
        <div class="flex items-center gap-3">
          <span class="text-xs text-gray-400 dark:text-dark-500">&copy; {{ currentYear }} {{ siteName }}. All rights reserved.</span>
        </div>
        <div class="flex items-center gap-4">
          <router-link to="/home" class="text-xs text-gray-400 transition-colors hover:text-gray-900 dark:text-dark-500 dark:hover:text-white">首页</router-link>
        </div>
      </div>
    </footer>
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue'
import { useAppStore } from '@/stores'

const appStore = useAppStore()

const siteName = computed(() => appStore.cachedPublicSettings?.site_name || appStore.siteName || '大灰狼')
const siteLogo = computed(() => appStore.cachedPublicSettings?.site_logo || appStore.siteLogo || '')
const currentYear = computed(() => new Date().getFullYear())
</script>
