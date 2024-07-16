<template>
    <div>
        <div
            class="link-card">
            <a :href="link" target="_blank" rel="noreferrer noopener"
                class="link-url">
                {{ link }}
            </a>
            <div
                class="copy-box">
                <button @click="copyToClipboard(link, 1)" :class="`copy-base ${copied ? 'bg-neutral-darkBlue' : 'bg-primary-cyan btn-hover'
                    }`">
                    {{ copied ? "Copied!" : "Copy" }}
                </button>
            </div>
        </div>
    </div>

</template>

<script setup>
import { ref } from 'vue'
const { link } = defineProps(['link'])
const copied = ref(false)

const copyToClipboard = (text) => {
    navigator.clipboard.writeText(text).then(() => {
        copied.value = true
        setTimeout(() => {
            copied.value = false
        }, 2000)
    }).catch((err) => {
        console.error('Failed to copy: ', err);
    });
};
</script>

<style scoped>
.link-card {
    @apply flex flex-col lg:flex-row lg:items-center lg:justify-between w-full lg:py-4 lg:px-5 bg-white rounded-md;
}
.link-url {
    @apply block break-words font-medium hover:text-neutral-grayishViolet pt-5 pb-4 px-4 sm:px-6 lg:p-0 border-b-2 lg:border-none border-solid border-gray-200 transition-colors;
}
.copy-base {
    @apply sm:w-28 text-white font-semibold py-3 px-8 sm:px-0 hover:bg-opacity-80 rounded-md transition-all;
}
.copy-box {
    @apply flex flex-col sm:flex-row sm:items-center sm:justify-between gap-4 pt-4 pb-6 sm:py-5 px-4 sm:px-6 lg:p-0;
}
</style>