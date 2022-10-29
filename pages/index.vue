<script setup>
const { data } = await useFetch('https://dummyjson.com/posts?limit=10')
const posts = data.value.posts
</script>

<template>
	<div class="mt-10 mx-auto grid grid-cols-3 gap-5">
		<Post :data="posts" />
	</div>
</template>
