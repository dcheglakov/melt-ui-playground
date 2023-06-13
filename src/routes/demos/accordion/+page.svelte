<script lang="ts">
	import { createAccordion } from '@melt-ui/svelte';
	import { slide } from 'svelte/transition';
	import { get } from 'svelte/store';

	const { content, item, trigger, isSelected, root } = createAccordion();

	const accordion = [
		{
			id: 'item-1',
			title: 'Is it accessible?',
			content: 'Yes. It adheres to the WAI-ARIA design pattern.'
		},
		{
			id: 'item-2',
			title: 'Is it unstyled?',
			content: "Yes. It's unstyled by default, giving you freedom over the look and feel."
		},
		{
			id: 'item-3',
			title: 'Can it be animated?',
			content: 'Yes! You can use the transition prop to configure the animation.'
		}
	];
	// const itemStore = get(item);
</script>

<div class="container m-auto py-12">
	<div class="w-full rounded-md overflow-hidden bg-[--line-color] shadow-lg" {...root}>
		{#each accordion as item}
			<div {...$item(item.id)} class="accordion-item">
				<h3 class="flex">
					<button {...$trigger(item.id)} class="accordion-trigger">{item.title}</button>
				</h3>
				{#if $isSelected(item.id)}
					<div class="accordion-content" {...$content(item.id)} transition:slide|local>
						<div class="px-5 py-4">{item.content}</div>
					</div>
				{/if}
			</div>
		{/each}
	</div>
</div>

<style lang="postcss">
	.accordion-item {
		@apply mt-px overflow-hidden first:mt-0 first:rounded-t last:rounded-b 
				focus-within:relative focus-within:z-10 focus-within:ring focus-within:ring-gray-400;
	}

	.accordion-trigger {
		@apply flex h-12 flex-1  cursor-pointer items-center
				justify-between bg-white px-5 text-base font-medium leading-none text-gray-700
				outline-none hover:bg-gray-100;
	}

	.accordion-content {
		@apply overflow-hidden bg-gray-100 text-sm text-gray-900;
	}
</style>
