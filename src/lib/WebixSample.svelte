<script lang="ts">
	import * as webix from 'webix';
	import { onDestroy, onMount } from 'svelte';
	import { movies } from '$lib/movies';

	const __ = globalThis.$$;
	let webixUI;

	let colorCode = '#860EFE';

	onMount(() => {
		let header = {
			view: 'template',
			type: 'header',
			template: `Webix Header uid:${webix.uid()}`,
			css: 'webix_dark'
		};

		let dataTable = {
			margin: 10,
			height: 830,
			width: 430,
			rows: [
				{
					view: 'datatable',
					id: 'movieTable',
					scrollY: false,
					autoConfig: true,
					columns: [
						{ id: 'rank', header: '#', width: 50, sort: 'int', css: 'rank' },
						{ id: 'title', header: 'Film title', width: 200, sort: 'string' },
						{ id: 'year', header: 'Released', width: 80, sort: 'int' },
						{ id: 'votes', header: 'Votes', width: 100, sort: 'int' }
					],
					pager: 'pagerA',
					select: true,
					yCount: 10,
					data: movies
				},
				{
					view: 'pager',
					id: 'pagerA',
					size: 10,
					group: 5
				},
				{
					view: 'form', id: 'form1', elements: [
						{ view: 'text', name: 'title', label: 'Title' },
						{ view: 'text', name: 'year', label: 'Year' },
						{
							view: 'button', value: 'Save', click: function() {
								const v1 = __('form1').getDirtyValues();
								__('form1').save(v1);
							}
						}
					]
				}
			]
		};

		let colorPickerRows = {
			rows:
				[
					{
						id: 'colorPicker',
						'label': 'Color',
						'value': colorCode,
						'view': 'colorpicker',
						on: {
							onChange: function(value) {
								colorCode = value;
							}
						}
					}
				]
		};

		webixUI = webix.ui({
			container: 'webixContainer',
			css: 'm-2',
			rows: [
				header,
				colorPickerRows,
				dataTable
			]
		});

		__('form1').bind(__('movieTable'));
	})
	;

	onDestroy(() => {
		webixUI.destructor();
	});

</script>

<div id="webixContainer"></div>
<div class="absolute bottom-1.5 text-center font-bold mx-2" style="color: {colorCode}">
	Color selection: {colorCode}
</div>