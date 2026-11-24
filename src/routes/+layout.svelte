<script>
	import "#lib/assets/favicon.ico";
	let { children } = $props();
	import "#lib/styles.css";
</script>

<svelte:head>
	<link rel="preconnect" href="https://fonts.googleapis.com">
	<link rel="preconnect" href="https://fonts.gstatic.com">
	<link href="https://fonts.googleapis.com/css2?family=Cal+Sans&family=Host+Grotesk:ital,wght@0,300..800;1,300..800&family=Montserrat:ital,wght@0,100..900;1,100..900&family=Playwrite+DK+Loopet:wght@100..400&display=swap" rel="stylesheet">
	<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@24,400,0,0&icon_names=arrow_circle_down,swipe_down" />

	<link rel="stylesheet" href="https://unpkg.com/@hackclub/theme@2/dist/hackclub.css" />
	<script type="module" src="https://unpkg.com/@hackclub/theme@2/dist/hackclub.js"></script>
</svelte:head>

{@render children()}
