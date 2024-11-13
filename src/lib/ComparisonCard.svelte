<script lang="ts">
	let {
		title,
		emoji,
		imageUrl,
		imageAlt,
		lightboxDescription
	}: {
		title: string
		emoji: string
		imageUrl: string
		imageAlt: string
		lightboxDescription: string
	} = $props()
	import { Lightbox } from 'svelte-lightbox'
	import MagnifierOverlay from '$lib/MagnifierOverlay.svelte'
</script>

<div
	class="flex h-full max-w-[30vw] flex-col border border-2 border-[var(--r-climate-rag-color)] bg-[var(--r-background-color)] p-2 xl:p-4"
>
	<h2 class="mb-5 text-xl xl:text-2xl">{title}</h2>
	<div class="text-xl xl:text-4xl">
		{emoji}
	</div>
	<div class="flex flex-col grow items-start justify-items-start p-4">
        <div class="font-bold self-start pb-2 border-b-2 border-[var(--r-climate-rag-color)]">Response</div>
		<div class=" bg-gray-500">
            <MagnifierOverlay>
                <Lightbox description={lightboxDescription}>
                    <img src={imageUrl} alt={imageAlt} />
                </Lightbox>
            </MagnifierOverlay>
            <div class="pt-2 pb-2 text-xs font-mono">{lightboxDescription}</div>
        </div>
	</div>
</div>
