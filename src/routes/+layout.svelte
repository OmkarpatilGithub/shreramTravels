<script lang="ts">
	import favicon from '$lib/assets/favicon.svg';
  import "../app.css";

	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href='/logo.png' />
</svelte:head>

{@render children()}
