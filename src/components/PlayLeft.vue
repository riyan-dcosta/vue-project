<script setup lang="ts">
import {  } from "vue";
const props = defineProps({
    message: String
})
</script>

<template>
    <main>
        <p>Hello there, I am PlayLeft child</p>
        <prem>Hopefully you will see me on the left side </prem>
        <p>{{ props.message }}</p>
    </main>
</template>

<style></style>