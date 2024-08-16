<script setup lang="ts">
const url = 'https://api.kanye.rest/text'

const { error, pending, data: quote } = await useFetch(url, { lazy: true })

async function fetQuotes() {
	const { error, pending, data: quotee } = await useFetch(url, { lazy: true })

	quote.value = quotee.value
}
</script>

<template>
	<div class="body-wrap min-h-screen bg-[#F9F7F7] w-full pt-20">
		<div class="container">
			<div class="body-inner max-w-xl mx-auto">
				<header class="text-center mb-10 space-y-2">
					<h1 class="text-2xl font-semibold">💡 Kanye Quotes</h1>
					<p class="text-xs text-[#adb3be]">
						Random Kanye West quotes (Kanye as a Service). REST API by
						<a href="https://x.com/andrewjazbec" class="text-blue-500">@andrewjazbec</a>
					</p>
				</header>
				<main>
					<div class="flex justify-between items-center text-sm p-2 space-x-4">
						<a href="http://api.kanye.rest" class="text-blue-500">https://api.kanye.rest</a>
						<nav class="items-center justify-between flex space-x-4">
							<span @click="fetQuotes()" class="cursor-pointer">🔄 refresh</span>
						</nav>
					</div>
					<div
						class="content mb-10 relative px-4 py-2 rounded-md font-semibold bg-[#DBE2EF] text-[#112D4E]"
					>
						<span v-if="pending">Loading...</span>
						<p v-else>{{ quote }}</p>
						<div class="flex w-full justify-end">
							<span class="author text-sm font-normal">- Kanye West</span>
						</div>
					</div>
				</main>
				<footer>
					<p class="text-center">
						<a href="https://github.com/abdullayevf" class="text-blue-500">👋 @abdullayevf</a>
					</p>
				</footer>

				<!-- Error message -->

				<p
					v-if="error"
					class="text-red-600 bg-red-200 absolute top-4 right-4 border-red-600 inline-block px-6 rounded-md py-4"
				>
					{{ error.cause }}
				</p>
			</div>
		</div>
	</div>
</template>

<style>
.body-wrap {
	font-family: Inter;
}
</style>
