<script lang="ts">
	import { createDialog } from '@melt-ui/svelte';
	import X from '~icons/lucide/x';

	const { trigger, portal, overlay, content, title, description, close, open } = createDialog({
		preventScroll: true
	});
	let y = 0;
</script>

<svelte:window bind:scrollY={y} />

<div class="container p-4 flex flex-col gap-8 items-start">
	<div class="h-screen">
		<header class=" rounded-md p-3 fixed top-4 {y === 0 ? 'bg-slate-100' : 'bg-red-100'}">
			Scroll down to open dialog
		</header>
	</div>
	<button
		{...$trigger}
		use:trigger
		class="inline-flex items-center justify-center rounded-md bg-white px-4 py-2
    font-medium leading-none text-magnum-700 shadow-lg hover:opacity-75"
	>
		Open Dialog
	</button>
</div>

<div use:portal>
	{#if $open}
		<div {...$overlay} use:overlay class="fixed inset-0 z-40 bg-black/50" />
		<div
			class="fixed left-[50%] top-[50%] z-50 max-h-[85vh] w-[90vw]
            max-w-[450px] translate-x-[-50%] translate-y-[-50%] rounded-md bg-white
            p-6 shadow-lg"
			{...$content}
			use:content
		>
			<h2 {...$title} use:title class="m-0 text-lg font-medium text-black">Edit profile</h2>
			<p {...$description} use:description class="mb-5 mt-2 leading-normal text-zinc-600">
				Make changes to your profile here. Click save when you're done.
			</p>

			<fieldset class="mb-4 flex items-center gap-5">
				<label class="w-[90px] text-right text-magnum-800" for="name"> Name </label>
				<input
					class="inline-flex h-8 w-full flex-1 items-center justify-center
                    rounded-sm border border-solid px-3 leading-none text-magnum-800"
					id="name"
					value="Thomas G. Lopes"
				/>
			</fieldset>
			<fieldset class="mb-4 flex items-center gap-5">
				<label class="w-[90px] text-right text-magnum-800" for="username"> Username </label>
				<input
					class="inline-flex h-8 w-full flex-1 items-center justify-center
                    rounded-sm border border-solid px-3 leading-none text-magnum-800"
					id="username"
					value="@thomasglopes"
				/>
			</fieldset>
			<div class="mt-6 flex justify-end gap-4">
				<button
					{...$close}
					use:close
					class="inline-flex h-8 items-center justify-center rounded-[4px]
                    bg-zinc-100 px-4 font-medium leading-none text-zinc-600"
				>
					Cancel
				</button>
				<button
					{...$close}
					use:close
					class="inline-flex h-8 items-center justify-center rounded-[4px]
                    bg-magnum-100 px-4 font-medium leading-none text-magnum-900"
				>
					Save changes
				</button>
			</div>

			<button
				{...$close}
				use:close
				aria-label="close"
				class="absolute right-[10px] top-[10px] inline-flex h-6 w-6
                appearance-none items-center justify-center rounded-full text-magnum-800
                hover:bg-magnum-100 focus:shadow-magnum-400"
			>
				<X />
			</button>
		</div>
	{/if}
</div>
