<script lang="ts">
	import { Search, Button, Alert } from 'flowbite-svelte';
    import { InfoCircleSolid } from 'flowbite-svelte-icons';
    import { fly } from 'svelte/transition';

	let searchQuery = '';
    let showSuccessAlert = false;
    let searchResult = '';

	async function handleSearch() {
		try {
			const response = await fetch(`/api/search?q=${searchQuery}`, {
				headers: { 'Content-Type': 'application/json' }
			});

			const data = await response.json();
			searchResult = JSON.stringify(data.url);
            showSuccessAlert = true;
            // Hide alert after 5 seconds
            setTimeout(() => {
                showSuccessAlert = false;
            }, 50000);
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
        {#if showSuccessAlert}
            <div transition:fly="{{ y: 20, duration: 300 }}">
                <Alert color="green" dismissable>
                    <InfoCircleSolid slot="icon" class="w-5 h-5" />
                    找到相關案例，請到下面網站幫你產生策略：<u><a href={searchResult} target="_blank">Grok 連結</a></u>
                </Alert>
            </div>
        {/if}
	</div>
</div>
