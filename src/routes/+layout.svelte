<script>
	import LibLoader from '$lib/LibLoader.svelte';

	function onLoaded() {
		console.log('WEBIX ready....');
	}
</script>

<LibLoader url="%sveltekit.assets%/webix/skin.js" on:loaded="{onLoaded}" />

<slot />
