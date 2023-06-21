<script lang="ts">
	import { fly } from 'svelte/transition';
</script>

<div
	transition:fly={{ y: 40 }}
	class="fixed inset-0 z-[110] m-auto flex h-fit max-w-sm flex-col gap-2 rounded-md bg-slate-100 p-4"
	{...$$props}
>
	<slot />
</div>
