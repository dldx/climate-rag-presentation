<script lang="ts">
	import '../styles/app.css'

	let { children } = $props()
</script>

<svelte:head>
	<title>Climate RAG</title>
</svelte:head>

{@render children()}