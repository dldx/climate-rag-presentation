<script lang="ts">
	import roadmap from '$lib/roadmap.svg?raw'
	import { Transition } from '@animotion/core'
	let { stepNo }: { stepNo: number } = $props()
</script>

<div
	style="--road-opacity:{stepNo >= 0 ? '1' : '0'};
	--reviewer-agent-opacity:{stepNo >= 0 ? '1' : '0'};
	--multi-hop-agent-opacity:{stepNo >= 1 ? '1' : '0'};
	--conversations-opacity:{stepNo >= 2 ? '1' : '0'};
	--image-retrieval-opacity:{stepNo >= 3 ? '1' : '0'};
	--sql-agent-opacity:{stepNo >= 4 ? '1' : '0'};
	--graph-agent-opacity:{stepNo >= 5 ? '1' : '0'};
	--dedicated-ui-opacity:{stepNo >= 6 ? '1' : '0'};
	"
>
	{@html roadmap}
</div>
{#each { length: 6 } as _, i}
	<Transition
		do={() => {
			stepNo = i + 1
		}}
		undo={() => {
			stepNo = i
		}}
	/>
{/each}

<style>
	:global(g[inkscape\:label='road']) {
		opacity: var(--road-opacity);
	}
	:global(g[inkscape\:label='reviewer-agent']) {
		opacity: var(--reviewer-agent-opacity);
	}
	:global(g[inkscape\:label='multi-hop-agent']) {
		opacity: var(--multi-hop-agent-opacity);
	}
	:global(g[inkscape\:label='conversations']) {
		opacity: var(--conversations-opacity);
	}
	:global(g[inkscape\:label='image-retrieval']) {
		opacity: var(--image-retrieval-opacity);
	}
	:global(g[inkscape\:label='sql-agent']) {
		opacity: var(--sql-agent-opacity);
	}
	:global(g[inkscape\:label='graph-agent']) {
		opacity: var(--graph-agent-opacity);
	}
	:global(g[inkscape\:label='dedicated-ui']) {
		opacity: var(--dedicated-ui-opacity);
	}
</style>
