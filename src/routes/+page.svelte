<script lang="ts">
    import { Search, Button } from 'flowbite-svelte';
    
    let searchQuery = '';

    async function handleSearch() {
        try {
            const response = await fetch('/api/search', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify({ query: searchQuery })
            });
            
            const data = await response.json();
            // Handle the response data here
            console.log(data);
        } catch (error) {
            console.error('Search failed:', error);
        }
    }
</script>

<div class="flex justify-center items-center min-h-screen">
    <div class="w-full max-w-2xl p-[5em]">
        <Search bind:value={searchQuery}>
            <Button class="me-1" on:click={handleSearch}>Search</Button>
        </Search>
    </div>
</div>
