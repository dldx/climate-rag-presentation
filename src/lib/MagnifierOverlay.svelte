<script lang="ts">
	import type { Snippet } from 'svelte'
	let {
		children
	}:{children: Snippet} = $props()
</script>

<div class="group relative">
	<div class="transition-opacity opacity-75 group-hover:opacity-100">{@render children()}</div>
	<div
		class="pointer-events-none absolute inset-0 flex items-center justify-center opacity-30 transition-opacity group-hover:opacity-100"
	>
		<svg
			xmlns="http://www.w3.org/2000/svg"
			class="h-12 w-12 text-white"
			fill="none"
			viewBox="0 0 24 24"
			stroke="currentColor"
		>
			<path
				stroke-linecap="round"
				stroke-linejoin="round"
				stroke-width="2"
				d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"
			/>
		</svg>
	</div>
</div>
