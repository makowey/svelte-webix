<script lang="ts">
	import * as webix from 'webix';
	import { onDestroy, onMount } from 'svelte';
	import { movies } from '$lib/movies';

	let components = [];
	let webixUI;

	onMount(() => {
		let header = {
			view: 'label',
			type: 'header',
			template: `Webix Header ${webix.uid()}`
		};

		let button = {
			view: 'button',
			value: 'demo'
		};

		let dataTable = {
			margin: 10,
			height: 830,
			width: 420,
			rows: [
				{
					view: 'pager',
					id: 'pagerA',
					size: 10,
					group: 5
				},
				{
					view: 'datatable',
					scrollY: false,
					columns: [
						{ id: 'rank', header: '#', width: 50, sort: 'int', css: 'rank' },
						{ id: 'title', header: 'Film title', width: 200, sort: 'string' },
						{ id: 'year', header: 'Released', width: 80, sort: 'int' },
						{ id: 'votes', header: 'Votes', width: 100, sort: 'int' }
					],
					pager: 'pagerA',
					select: true, yCount: 10,
					autowidth: true,
					data: movies
				}
			]
		};

		webixUI = webix.ui({
			container: 'webixContainer',
			rows: [
				header,
				button,
				dataTable
			]
		});
	});

	onDestroy(() => {
		webixUI.destructor();
	});

</script>

<div id="webixContainer"></div>