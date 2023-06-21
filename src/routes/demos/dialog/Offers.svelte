<script lang="ts">
	import { createTabs } from '@melt-ui/svelte';
	import Offer from './Offer.svelte';
	import OfferTab from './OfferTab.svelte';

	export let offers: OfferType[];
	const { root, list, content, trigger } = createTabs({ value: 'tab1' });

	const singleOffers = offers.filter((offer) => offer.type < 16);
	const onDemandOffers = offers.filter((offer) => offer.type >= 16);
</script>

<section {...$root}>
	<div {...$list} class="grid grid-cols-1 gap-3 md:grid-cols-2" aria-label="Choose the offer type">
		<OfferTab {...$trigger('tab1')}>
			Single Lesson
			<svelte:fragment slot="description">Get one-off instruction as needed</svelte:fragment>
		</OfferTab>
		<OfferTab {...$trigger('tab2')}>
			Coach On-Demand
			<svelte:fragment slot="description">Get monthly lesson packages & deals</svelte:fragment>
		</OfferTab>
	</div>
	<div {...$content('tab1')}>
		<div class="grid grid-cols-1 gap-4 pt-4 text-lg text-slate-600 md:grid-cols-2">
			{#each singleOffers as offer}
				<Offer {offer} />
			{/each}
		</div>
	</div>
	<div {...$content('tab2')}>
		<div class="grid grid-cols-1 gap-4 pt-4 text-lg text-slate-600 md:grid-cols-2">
			{#each onDemandOffers as offer}
				<Offer {offer} />
			{/each}
		</div>
	</div>
</section>
