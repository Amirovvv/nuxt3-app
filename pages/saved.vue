<script setup>
import { ArrowLeftCircleIcon } from '@heroicons/vue/24/solid'

const save = useSave()
</script>

<template>
	<div class="mt-10 mx-auto max-w-prose grid gap-5">
		<NuxtLink
			to="/"
			class="flex items-center text-2xl font-medium text-indigo-500 hover:text-indigo-400"
		>
			<ArrowLeftCircleIcon class="w-6 h-6 mr-1" />
			Back to post list
		</NuxtLink>
		<span class="text-white font-medium text-3xl">Saved posts</span>
		<Post :data="save" />
		<span v-if="!save.length" class="text-gray-300 mt-10 mx-auto"
			>You don't have any saved posts</span
		>
	</div>
</template>
