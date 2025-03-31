<script setup lang="ts">
import type { NuxtError } from '#app';

const { error } = defineProps<{ error: NuxtError }>()

const handleError = () => {
  clearError({
    redirect: '/course/chapter/1-chapter-1/lesson/1-introduction-to-typescript-with-vue-js-3'
  })
}
</script>

<template>
  <NuxtLayout>
    <div>
      <h1>Dang</h1>
      <p>It looks like something broke</p>
      <p class="font-bold">{{ error.message }}</p>
      <p>
        Go to the
        <a class="hover:cursor-pointer" @click="handleError">
          first lesson
        </a>
      </p>
    </div>
  </NuxtLayout>
</template>