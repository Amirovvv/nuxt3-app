<script setup>
const { data } = await useFetch('https://dummyjson.com/posts?limit=10')
const posts = data.value.posts
const tags = ref([])

const activeTag = ref('')

function activateTag(tag) {
  if (activeTag.value == tag) {
    activeTag.value = ''
    return
  }
  activeTag.value = tag
}

function getTags() {
  let array = []
  posts.forEach((post) => {
    post.tags.forEach((tag) => {
      array.push(tag)
    })
  })
  tags.value = new Set(array)
}

const filteredPosts = computed(() => {
  if (activeTag.value) {
    return posts.filter((post) => {
      return post.tags.includes(activeTag.value)
    })
  }
  return posts
})

getTags()
</script>

<template>
  <div class="mt-10 mx-auto">
    <div>
      <span class="text-white mr-2">Sorting by tags :</span>
      <span
        class="px-2 py-1 mr-2 cursor-pointer rounded-full text-sm text-indigo-100 font-medium bg-indigo-900 hover:bg-indigo-500"
        v-for="tag in tags"
        :key="tag"
        :class="[activeTag === tag ? 'bg-indigo-500' : '']"
        @click="activateTag(tag)"
        >{{ tag }}</span
      >
    </div>
    <div class="mt-5 grid grid-cols-3 gap-5">
      <Post :data="filteredPosts" />
    </div>
  </div>
</template>
