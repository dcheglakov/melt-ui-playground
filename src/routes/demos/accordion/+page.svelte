<script lang="ts">
	import { createAccordion } from '@melt-ui/svelte';
	import { slide } from 'svelte/transition';

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
</script>

<div class="container m-auto py-12">
	<div {...root}>
		{#each accordion as accordionItem, i}
			<div {...$item(accordionItem.id)}>
				<h3>
					<button
						{...$trigger(accordionItem.id)}
						class="flex gap-2 items-center w-full text-left px-3 py-2 hover:bg-gray-100 transition-colors rounded-md {$isSelected(
							accordionItem.id
						)
							? 'bg-gray-100'
							: ''}"
						>{(i + 1).toString().padStart(2, '0')}.<span class="flex-1">{accordionItem.title}</span>
						{$isSelected(accordionItem.id) ? '-' : '+'}</button
					>
				</h3>
				{#if $isSelected(accordionItem.id)}
					<div {...$content(accordionItem.id)} transition:slide|local class="px-4">
						<p class="border-l-2 border-gray-100 py-2 px-3">{accordionItem.content}</p>
					</div>
				{/if}
			</div>
		{/each}
	</div>
</div>
