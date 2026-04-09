<script lang="ts">
	import '../app.css';
	let { children } = $props();
	const siteUrl = 'https://uw2026leanhackathon.github.io';
</script>

<svelte:head>
	<meta name="description" content="UW Lean Hackathon 2026 — A two-day hackathon showcasing the power of the Lean Proof Assistant. May 8–10, 2026 at the University of Washington." />
	<meta name="robots" content="index, follow" />
	<link rel="canonical" href={siteUrl} />
	<meta property="og:url" content={siteUrl} />
	<title>UW Lean Hackathon 2026</title>
</svelte:head>

{@render children()}
