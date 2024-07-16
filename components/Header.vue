<template>
  <header class="header">
    <NuxtImg src="images/logo.svg" width="120px" alt="Shortly" />

    <button aria-label="menu-btn" aria-controls="menu" aria-expanded={menuVisible}
      class="lg:hidden flex flex-col gap-[5.5px] w-9 h-8 p-1 focus:outline-2 focus:outline-offset-4 rounded-sm" @click="() => {
        menuVisible = !menuVisible
      }">
      <span class="block w-full h-1 bg-neutral-gray rounded"></span>
      <span class="block w-full h-1 bg-neutral-gray rounded"></span>
      <span class="block w-full h-1 bg-neutral-gray rounded"></span>
    </button>

    <nav id="menu" :class="`nav-base bg-primary-darkVoilet
      ${menuVisible
        ? 'scale-100 translate-x-0 translate-y-0'
        : 'scale-0 translate-x-36 -translate-y-48'
      }
      `">
      <ul class="flex flex-col lg:flex-row items-center lg:text-neutral-grayishViolet">
        <li>
          <NuxtLink href="/"
            class="nav-item">
            Features
          </NuxtLink>
        </li>
        <li>
          <NuxtLink href="/"
            class="nav-item">
            Pricing
          </NuxtLink>
        </li>
        <li>
          <NuxtLink href="/"
            class="nav-item">
            Resources
          </NuxtLink>
        </li>
      </ul>

      <div
        class="login-box">
        <NuxtLink href="/"
          class="login-btn">
          Login
        </NuxtLink>
        <NuxtLink href="/"
          class="signup-btn bg-primary-cyan">
          Sign Up
        </NuxtLink>
      </div>
    </nav>
  </header>
</template>

<script setup>
import { ref } from 'vue'
const menuVisible = ref(false)


</script>

<style scoped>
.header {
  @apply relative flex justify-between lg:justify-start items-center lg:gap-8 xl:gap-12 py-6 lg:py-8 px-5 lg:px-20 xl:px-36;
}

.nav-base {
  @apply absolute lg:static top-20 right-5 left-5 sm:left-auto flex flex-col lg:flex-row lg:justify-between items-center sm:w-[360px] lg:w-full text-white lg:text-black font-medium py-6 px-5 lg:p-0 lg:bg-transparent rounded-xl lg:scale-100 lg:translate-x-0 lg:translate-y-0 transition-all;
}

.nav-item {
  @apply inline-block lg:font-semibold hover:text-black py-3 px-4 rounded-md transition-colors;
}

.login-box {
  @apply flex flex-col lg:flex-row items-center gap-3 w-full lg:w-auto pt-7 pb-3 lg:py-0 border-t border-solid lg:border-none border-[#8f78c9] mt-4 lg:mt-0;
}

.login-btn {
  @apply inline-block font-semibold lg:text-neutral-grayishViolet lg:hover:text-black lg:py-2.5 lg:px-8 rounded-md transition-colors;
}

.signup-btn {
  @apply inline-block text-white font-semibold py-2.5 px-8 lg:hover:bg-opacity-50 rounded-full transition-colors;
}
</style>