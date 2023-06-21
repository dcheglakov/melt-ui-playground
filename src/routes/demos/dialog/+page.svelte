<script lang="ts">
	import Offers from './Offers.svelte';
	const offers = [
		{
			id: 1,
			title: 'Live Call',
			description:
				'Send footage from practice sessions or games, and your coach will use telestrated drawings, pro-player comparisons, voiceovered insights, and in-picture coach demonstrations to breakdown your technique and provide truly personal feedback.',
			price: '$49.99',
			href: 'https://www.apple.com',
			customDetails: '30 minutes',
			type: 1
		},
		{
			id: 2,
			title: 'In-Person',
			description:
				'Send footage from practice sessions or games, and your coach will use telestrated drawings, pro-player comparisons, voiceovered insights, and in-picture coach demonstrations to breakdown your technique and provide truly personal feedback.',
			price: '$79.99',
			href: 'https://www.apple.com',
			customDetails: '130 minutes',
			type: 2
		},
		{
			id: 3,
			title: 'Full Remote',
			description:
				'Send footage from practice sessions or games, and your coach will use telestrated drawings, pro-player comparisons, voiceovered insights, and in-picture coach demonstrations to breakdown your technique and provide truly personal feedback.',
			price: '$499.99',
			href: 'https://www.apple.com',
			customDetails: '45 minutes',
			type: 16
		},
		{
			id: 4,
			title: 'Analysis',
			description:
				'Send footage from practice sessions or games, and your coach will use telestrated drawings, pro-player comparisons, voiceovered insights, and in-picture coach demonstrations to breakdown your technique and provide truly personal feedback.',
			price: '$799.99',
			href: 'https://www.apple.com',
			customDetails: '130 minutes',
			type: 18
		}
	];
</script>

<Offers {offers} />
