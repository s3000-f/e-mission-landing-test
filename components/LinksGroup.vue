<template>
    <div class="mt-8 w-full mx-auto">
        <LinkCard v-for="link in links" :link="link" class="mb-4" />
    </div>
</template>

<script setup>
const { links } = defineProps(['links'])
</script>
