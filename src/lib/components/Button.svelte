<script lang="ts">
	import { cva, type VariantProps } from 'class-variance-authority';
	export const preload: boolean = false;
	export let href: string | undefined = undefined;
	export let isBranded: boolean = false;
	export let disabled: boolean = false;
	export let progress: boolean = false;
	let className: string | undefined = '';
	export let noscroll: true | '' | 'off' | null | undefined = 'off';
	export { className as class };
	const style = isBranded
		? 'background-color: var(--color, #EB0000); color: var(--text, #fff)'
		: '';

	const button = cva(
		[
			'w-full items-center justify-center whitespace-nowrap sm:w-auto inline-flex gap-1 rounded-xl leading-none px-12 py-4 uppercase tracking-wide font-medium text-sm transition-all',
			className,
			'disabled:opacity-50 disabled:cursor-not-allowed'
		],
		{
			variants: {
				variant: {
					primary: 'bg-brand-dark hover:bg-brand text-white disabled:bg-brand-dark',
					secondary: 'bg-black hover:outline-black text-white disabled:bg-black',
					gray: 'bg-slate-100 hover:bg-slate-200 text-slate-800 disabled:bg-slate-100'
				}
			},
			defaultVariants: {
				variant: 'primary'
			}
		}
	);

	type ButtonProps = VariantProps<typeof button>;
	export let variant: ButtonProps['variant'] = undefined;
</script>

{#if href}
	<a
		{...$$props}
		{href}
		class={button({ variant })}
		data-sveltekit-preload-data
		data-sveltekit-noscroll={noscroll}
		{style}
	>
		{#if progress}
			Loading...
		{:else}
			<slot />
		{/if}
	</a>
{:else}
	<button {...$$props} {style} on:click class={button({ variant })} {disabled}><slot /></button>
{/if}
