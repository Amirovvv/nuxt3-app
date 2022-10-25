<template>
	<div class="text-red-100">{{ post.title }}</div>
</template>

<script setup>
const route = useRoute()
const data = await useFetch(`https://dummyjson.com/posts/${route.params.id}`, {
	transform: (data) => data,
	key: `post-transform-${route.params.id}`,
})
const post = ref(data.data.value)
</script>
