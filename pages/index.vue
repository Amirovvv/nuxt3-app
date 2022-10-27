<script setup>
const { data } = await useFetch('https://dummyjson.com/posts?limit=10')
const posts = data.value.posts

function savePost(post) {
	console.log(post)
}
</script>

<template>
	<div class="mt-10 mx-auto grid grid-cols-3 gap-5">
		<NuxtLink
			v-for="post in posts"
			:key="post.id"
			:to="{ name: 'post-id', params: { id: post.id } }"
			style="min-height: 136px"
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
						class="mt-2 inline-flex items-center px-2 py-1 mr-2 rounded-full text-sm text-indigo-100 font-medium bg-indigo-900"
						>{{ tag }}</span
					>
				</div>
			</div>
			<div class="ml-2">
				<IconsIconSaved
					class="w-8 h-8"
					:color="'none'"
					:stroke="'#ffffff'"
					@click.prevent="savePost(post)"
				/>
			</div>
		</NuxtLink>
	</div>
</template>
