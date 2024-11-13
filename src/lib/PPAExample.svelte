<script lang="ts">
	import ppaexample from '$lib/ppa-example.svg?raw'
	import { Transition } from '@animotion/core'
	import { draggable } from '@neodrag/svelte'
	let { stepNo }: { stepNo: number } = $props()
</script>

<div
	style="--countries-opacity:{stepNo >= 1 ? '1' : '0'};
	--question-opacity:{stepNo >= 2 ? '1' : '0'};
	--climate-rag-opacity:{stepNo >= 3 ? '1' : '0'};
	--other-countries-opacity:{stepNo >= 4 ? '1' : '0'};
	--gemini-opacity:{stepNo >= 5 ? '1' : '0'};
	--final-result-opacity:{stepNo >= 6 ? '1' : '0'};"
>
	{@html ppaexample}
</div>
{#if stepNo > 0}
	<div
		class="pointer-events-none absolute top-0 left-0 flex h-screen w-screen items-center justify-center"
	>
		<div
			use:draggable={{ bounds: 'body', cancel: '.cancel' }}
			class="pointer-events-auto absolute left-10 flex max-h-[80%] max-w-[35ch] cursor-grab flex-col gap-4 overflow-auto border-2 p-4 text-left text-sm backdrop-blur xl:text-xl"
			style="transition: unset !important; border-color: var(--r-heading-color); box-shadow: 5px 5px 0px 0px rgba(37, 178, 100, 0.3); background-color: rgba(20,20,20,0.9);"
		>
			<div class="cancel cursor-auto">
				{#if stepNo == 1}
					<ul class="list-none pl-5">
						<li>Run one Climate-RAG query per country in the question to get reliable results.</li>
					</ul>
				{/if}
				{#if stepNo == 2}
					<ul class="list-none pl-5">
						<li>For each country, create a question using a simple template.</li>
					</ul>
				{/if}
				{#if stepNo == 3}
					<ul class="list-none pl-5">
						<li>
							Run each query through Climate-RAG's tooling and let Climate-RAG track all the
							responses in its database.
						</li>
						<li>
							Other solutions may require you to manually enter each query into a website and
							manually track responses.
						</li>
					</ul>
				{/if}
				{#if stepNo == 4}
					<ul class="list-none pl-5">
						<li>Do the same for all the countries we care about.</li>
					</ul>
				{/if}
				{#if stepNo == 5}
					<ul class="list-none pl-5">
						<li>
							Use tooling to collate all the responses, along with citation info, and pass them into
							Google Gemini, which can handle very large inputs.
						</li>
						<li>Gemini can produce a publication-ready table</li>
					</ul>
				{/if}
				{#if stepNo == 6}
					<ul class="list-none pl-5">
						<li>
							The final result contains all relevant information, including citations of all
							documents referenced in the original queries.
						</li>
					</ul>
				{/if}
				{#if stepNo == 7}
					<ul class="list-none pl-5">
						<li>This multi-agent workflow will be built into Climate-RAG in the near future</li>
					</ul>
				{/if}
			</div>
		</div>
	</div>
{/if}
{#each { length: 6 } as _, i}
	<Transition
		do={() => {
			stepNo = i + 2
		}}
		undo={() => {
			stepNo = i + 1
		}}
	/>
{/each}

<style>
	:global(g[inkscape\:label='countries']) {
		opacity: var(--countries-opacity);
	}
	:global(g[inkscape\:label='other-countries']) {
		opacity: var(--other-countries-opacity);
	}
	:global(g[inkscape\:label='question']) {
		opacity: var(--question-opacity);
	}
	:global(g[inkscape\:label='climate-rag']) {
		opacity: var(--climate-rag-opacity);
	}
	:global(g[inkscape\:label='gemini']) {
		opacity: var(--gemini-opacity);
	}
	:global(g[inkscape\:label='final-result']) {
		opacity: var(--final-result-opacity);
	}

	div {
		transition: all 0.5s ease;
	}
</style>
