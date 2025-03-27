<script lang="ts">
	import { Search, Button } from 'flowbite-svelte';

	let searchQuery = '';

	async function handleSearch() {
		try {
			const response = await fetch(`/api/search?q=${searchQuery}`, {
				headers: { 'Content-Type': 'application/json' }
			});

			const data = await response.json();
			// Handle the response data here
			console.log(data);
		} catch (error) {
			console.error('Search failed:', error);
		}
	}
</script>

<div class="flex min-h-screen items-center justify-center">
	<div class="w-full max-w-2xl p-[5em]">
		<Search bind:value={searchQuery}>
			<Button class="me-1" on:click={handleSearch}>描述你想說服的對象，跟你的狀況</Button>
		</Search>
	</div>
</div>
