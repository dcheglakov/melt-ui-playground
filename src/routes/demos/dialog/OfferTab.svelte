<button
	{...$$restProps}
	class="flex items-center justify-between rounded-lg border-2 bg-gray-50 px-5 py-4 text-left text-lg font-medium text-slate-800 data-[state=active]:border-brand data-[state=active]:bg-white"
>
	<span>
		<slot />
		<span class="block text-sm text-gray-600"><slot name="description" /></span>
	</span>
	<slot name="icon" />
</button>
