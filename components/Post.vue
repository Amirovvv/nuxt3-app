<script setup>
const props = defineProps({
  data: { type: Array },
})

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
  <NuxtLink
    v-for="post in data"
    :key="post.id"
    :to="{ name: 'post-id', params: { id: post.id } }"
    style="min-height: 136px"
    class="text-white flex justify-between bg-slate-800 rounded-lg shadow-lg p-6 hover:-translate-y-1.5"
    ><div class="flex flex-col justify-between">
      <div>
        <p class="text-xl font-semibold text-grat-900">
          {{ post.title }}
        </p>
      </div>
      <div>
        <span
          v-for="tag in post.tags"
          :key="tag"
          class="mt-2 inline-flex items-center px-2 py-1 mr-2 rounded-full text-sm text-indigo-100 font-medium bg-indigo-900"
          >{{ tag }}</span
        >
      </div>
    </div>
    <div class="ml-2">
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
  </NuxtLink>
</template>
