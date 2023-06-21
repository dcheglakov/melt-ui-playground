<script lang="ts">
	import { fade } from 'svelte/transition';
	import { createDialog } from '@melt-ui/svelte';

	import LucideActivity from '~icons/lucide/activity';
	import LucideMapPin from '~icons/lucide/map-pin';
	import LucidePlayCircle from '~icons/lucide/play-circle';
	import LucideVideo from '~icons/lucide/video';
	import LucideX from '~icons/lucide/x';

	import type { OfferType } from '../../../app';
	import Button from '$lib/components/Button.svelte';
	// Dialog Components
	import Overlay from '$lib/components/Dialog/Overlay.svelte';
	import Content from '$lib/components/Dialog/Content.svelte';
	import Title from '$lib/components/Dialog/Title.svelte';
	import Description from '$lib/components/Dialog/Description.svelte';
	import CloseButton from '$lib/components/Dialog/CloseButton.svelte';

	export let offer: OfferType;

	let dialogTitle = 'Download the app';
	let dialogDescription = `Scan this QR code with your iPhone or iPad’s camera, then follow the instructions to
						download the free app.`;

	const { trigger, portal, overlay, content, title, description, close, open } = createDialog();

	const getIcon = (type: string) => {
		switch (type) {
			case 'Live Call':
				return LucideVideo;
			case 'Analysis':
				return LucideActivity;
			case 'In-Person':
				return LucideMapPin;
			case 'Full Remote':
				return LucidePlayCircle;
			default:
				return LucideX;
		}
	};
</script>

<div class="flex flex-col rounded-lg bg-white p-4">
	<header
		class="mb-2 flex items-center justify-between border-b border-dashed border-slate-200 pb-2"
	>
		<h3 class="flex items-center gap-2 text-lg font-semibold text-slate-600">
			<svelte:component this={getIcon(offer.title)} class="h-6 w-6" />
			<span class="shrink-0" style="color: var(--color)" />
			{offer.title}
		</h3>
		<strong class="text-base font-medium text-sky-800">{offer.price}</strong>
	</header>
	<p class="h-full pb-4 text-base text-slate-500">{offer.description}</p>
	<footer class="flex flex-col gap-2">
		{#if offer.customDetails}
			<Button
				variant="gray"
				{...$trigger()}
				on:click={() => {
					dialogTitle = 'Coach Notes';
				}}>Coach Notes</Button
			>
		{/if}
		<Button
			isBranded
			{...$trigger()}
			on:click={() => {
				dialogTitle = 'Install the SeamsUp App';
			}}>Book with app</Button
		>
	</footer>
</div>

<div use:portal>
	{#if $open}
		<div
			{...$$props}
			class="fixed inset-0 z-[100] bg-black/50"
			transition:fade|local={{ duration: 150 }}
		/>
		<Overlay {...$overlay} />
		<Content {...$content}>
			<Title {...title}>
				{dialogTitle}
				<svelte:fragment slot="actions">
					<CloseButton {...$close()} />
				</svelte:fragment>
			</Title>
			<div class="flex flex-col gap-4">
				{#if dialogTitle === 'Coach Notes'}
					<Description {...description}>{offer.customDetails}</Description>
				{:else if dialogTitle === 'Install the SeamsUp App'}
					<Description>{dialogDescription}</Description>
				{/if}
			</div>
		</Content>
	{/if}
</div>
