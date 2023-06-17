<script lang="ts">
	import { createSelect } from '@melt-ui/svelte';
	import Check from '~icons/lucide/check';
	import ChevronDown from '~icons/lucide/chevron-down';

	const { selectedText, trigger, menu, option, isSelected } = createSelect();

	const options = {
		fruits: ['Apple', 'Banana', 'Pineapple'],
		vegetables: ['Broccoli', 'Potato', 'Tomato']
	};
</script>

<div class="m-4 p-4 rounded-lg bg-gray-100 flex gap-3">
	<button
		class="bg-white rounded-md border-gray-300 border flex justify-between items-center gap-2 px-3 py-2 w-48"
		{...$trigger}
		aria-label="Food"
	>
		{$selectedText || 'Select an option'}
		<ChevronDown />
	</button>

	<ul class="bg-white rounded-md border border-gray-300 shadow-md" {...$menu}>
		{#each Object.entries(options) as [key, arr]}
			<li class="uppercase text-xs px-3 text-gray-500 pt-3">{key}</li>
			{#each arr as item}
				<li class="px-3 py-2 flex justify-between items-center" {...$option({ value: item })}>
					{item}
					{#if $isSelected(item)}
						<Check />
					{/if}
				</li>
			{/each}
		{/each}
	</ul>

	<button class="px-3 py-2 bg-sky-200 text-sky-950 rounded-md">Focus test</button>
</div>
