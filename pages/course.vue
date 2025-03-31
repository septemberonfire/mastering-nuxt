<script setup>
const { chapters } = useCourse()

const resetError = async (error) => {
  await navigateTo('course/chapter/1-chapter-1/lesson/1-introduction-to-typescript-with-vue-js-3')
  error.value = null
}
</script>

<template>
  <div class="mb-12">
    <h1>
      <span class="font-medium">
        Course: <span class="font-bold">Mastering Nuxt 3</span>
      </span>
    </h1>
  </div>

  <div class="flex justify-center flex-grow">
    <div class="mr-4 p-8 bg-white rounded-md min-w-[20ch] max-w-[30ch] flex flex-col">
      <h3 class="font-bold mb-4">Chapters</h3>
      <div
        v-for="chapter in chapters"
        :key="chapter.slug"
        class="space-y-1 mb-4 flex flex-col"
      >
        <h4>{{ chapter.title }}</h4>
        <NuxtLink
          v-for="(lesson, index) in chapter.lessons"
          :key="lesson.slug"
          class="flex flex-row space-x-1 no-underline font-normal py-1 px-4 -mx-4 cursor-pointer"
          :to="lesson.path"
          :class="[
            lesson.path === $route.fullPath ? 'text-blue-500' : 'text-gray-600'
          ]"
        >
          <span class="text-gray-500">{{ index + 1 }}.</span>
          <span>{{ lesson.title }}</span>
        </NuxtLink>
      </div>
    </div>

    <div class="p-12 bg-white rounded-md min-w-[65ch]">
      <NuxtErrorBoundary>
        <NuxtPage />
        <template #error="{ error }">
          <p>
            oh no, something went wrong with the lesson
            <code>{{ error }}</code>
          </p>
          <p>
            <button
              class="hover:cursor-pointer bg-gray-500 text-white font-bold"
              @click="resetError(error)"
            >
              Reset
            </button>
          </p>
        </template>
      </NuxtErrorBoundary>
    </div>
  </div>
</template>