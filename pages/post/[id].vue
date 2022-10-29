<script setup>
import { ArrowLeftCircleIcon } from '@heroicons/vue/24/solid'

const route = useRoute()

const data = await useFetch(`https://dummyjson.com/posts/${route.params.id}`, {
  key: `post-${route.params.id}`,
})
const post = ref(data.data.value)

const save = useSave()

function isInSaved(post) {
  return !!save.value.find((se) => se.id === post.id)
}

function savePost(post) {
  if (!isInSaved(post)) {
    save.value.push(post)
  } else {
    save.value = save.value.filter((se) => se.id !== post.id)
  }
}
</script>

<template>
  <div class="text-2xl mx-auto mt-6 max-w-prose text-white">
    <NuxtLink
      to="/"
      class="flex items-center font-medium text-indigo-500 hover:text-indigo-400"
    >
      <ArrowLeftCircleIcon class="w-6 h-6 mr-1" />
      Back to post list
    </NuxtLink>
    <span
      class="mt-8 block text-4xl font-extrabold text-gray-100 tracking-tight"
      >{{ post.title }}</span
    >
    <div class="flex justify-between items-center mt-6">
      <div class="text-lg">
        <span class="mr-2">tags:</span>
        <span
          v-for="tag in post.tags"
          :key="tag"
          class="inline-flex items-center px-2 py-1 mr-2 rounded-full text-base text-indigo-100 font-medium bg-indigo-900"
          >{{ tag }}</span
        >
      </div>
      <IconsIconSaved
        v-if="isInSaved(post)"
        class="w-8 h-8"
        :color="'#ffffff'"
        :stroke="'#ffffff'"
        @click.prevent="savePost(post)"
      />
      <IconsIconSaved
        v-else
        class="w-8 h-8"
        :color="'none'"
        :stroke="'#ffffff'"
        @click.prevent="savePost(post)"
      />
    </div>
    <span class="mt-6 block">
      {{ post.body }}
    </span>
  </div>
</template>
