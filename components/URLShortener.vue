<template>
  <div class="mx-5 lg:mx-20 xl:mx-36 mt-16">
    <div class="url-shortener ">
      <div class="w-full relative">

        <input type="text" name="url" id="url" v-model="url" @focus="showError = false"
          :class="`url-input ${showError ? 'border-secondary-red' : 'border-transparent'}`" />
        
        <span :class="`url-placeholder text-neutral-grayishViolet ${url !== ''
          && 'left-10 opacity-0 invisible'} ${showError && 'text-secondary-red'}`">
          Shorten a url here...
        </span>

        <span :class="`absolute -bottom-6 z-30 left-2 w-max text-secondary-red text-sm transition-all duration-300
            ${showError ? 'visible opacity-100' : 'invisible opacity-0'}`">
          Please add valid a url

        </span>
      </div>

      <button @click="shortenLink()"
        class="w-full md:w-[180px] text-white font-semibold py-3 md:py-4 px-4 md:px-8 bg-primary-cyan hover:bg-[#63dddd] rounded-md transition-colors duration-200">
        Shorten it!
      </button>
    </div>

    <div :aria-live="links.length !== 0 ? 'polite' : 'off'" class="flex flex-col gap-5 mt-5">
      <LinksGroup :links="links" />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import LinksGroup from './LinksGroup.vue';
const toast = useToast()


const url = ref('')
const showError = ref(false)
let links = ref([])


const shortenLink = () => {
  if (!isValidURL(url.value)) {
    showError.value = true
  } else {
    showError.value = false
    links.value.push(url.value);
    toast.add({ title: 'Link shortened successfully' })
  }
}

const isValidURL = (str) => {
  const expression = /[-a-zA-Z0-9@:%._\+~#=]{1,256}\.[a-zA-Z0-9()]{1,6}\b([-a-zA-Z0-9()@:%_\+.~#?&//=]*)/gi;
  const regex = new RegExp(expression);
  return str.length < 2083 && str.match(regex);
}
</script>


<style scoped>
.url-input {
  @apply w-full py-3 md:py-4 px-4 md:px-7 border-4 border-solid rounded-md focus:outline-none transition-all duration-300;
}

.url-placeholder {
  @apply placeholder-text absolute top-1/2 left-4 md:left-7 -translate-y-1/2 font-medium text-sm transition-all duration-300 pointer-events-none;
}

.url-shortener {
  background-image: url(images/bg-shorten-mobile.svg);
  @apply flex flex-col md:flex-row gap-7 py-8 md:py-10 px-6 md:px-12 rounded-lg bg-no-repeat bg-cover bg-right-top md:bg-left-top;
  background-color: hsl(257, 27%, 26%);
}

.url-shortener input:focus~.placeholder-text {
  @apply left-10 opacity-0 invisible;
}


@media only screen and (min-width: 768px) {
  .url-shortener {
    background-image: url(images/bg-shorten-desktop.svg);
  }
}

.background-cyan {
  background-color: hsl(180 66% 49%);
}
</style>