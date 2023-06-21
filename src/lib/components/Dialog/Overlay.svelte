<script lang="ts">
	import { fade } from 'svelte/transition';
</script>

<div
	{...$$props}
	class="fixed inset-0 z-[100] bg-black/50"
	transition:fade|local={{ duration: 150 }}
/>
