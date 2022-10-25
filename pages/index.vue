<script setup>
const { data } = await useFetch('https://dummyjson.com/posts?limit=10')
const posts = toRaw(data.value.posts)
</script>

<template>
	<div class="mt-10 mx-auto grid grid-cols-3 gap-5">
		<NuxtLink
			v-for="post in posts"
			:to="`/post/${post.id}`"
			:key="post.title"
			style="height: 136px"
			class="text-white flex justify-between bg-slate-800 rounded-lg shadow-lg p-6"
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
						class="mt-2 inline-flex items-center px-2 py-1 mr-2 rounded-full text-xs text-indigo-100 font-medium bg-indigo-900"
						>{{ tag }}</span
					>
				</div>
			</div>
			<div class="ml-2" style="height: 40px">
				<IconsIconSaved :color="'#fff'" />
			</div>
		</NuxtLink>
	</div>
</template>
