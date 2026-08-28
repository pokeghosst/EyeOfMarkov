<script lang="ts">
	import CorpusDropdown from './CorpusDropdown.svelte';
	import NValue from './NValue.svelte';
	import Slider from './Temperature.svelte';

	const myItems = [
		{ value: 2, label: '2' },
		{ value: 3, label: '3' },
		{ value: 4, label: '4' },
		{ value: 5, label: '5' }
	];

	let temperature = $state(0.1);
	let nValue = $state(myItems[0].value);
</script>

<div class="toolbar">
	<CorpusDropdown />
	<div class="divider"></div>
	<NValue items={myItems} bind:value={nValue} name="n-value" />
	<Slider bind:value={temperature} min={0} max={1} step={0.1} type="single" />
</div>

<style>
	.toolbar {
		position: relative;
		z-index: 2;
		display: flex;
		align-items: flex-end;
		gap: 20px;
		padding: 16px 28px;
		background: var(--bg-surface);
		border-bottom: 1px solid var(--border);
	}

	.divider {
		width: 1px;
		align-self: stretch;
		background: var(--border);
	}
</style>
