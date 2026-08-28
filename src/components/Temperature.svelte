<script lang="ts">
	/* eslint-disable @typescript-eslint/no-explicit-any */

	import type { ComponentProps } from 'svelte';
	import { Slider, type WithoutChildren } from 'bits-ui';
	import Label from './Label.svelte';

	type Props = WithoutChildren<ComponentProps<typeof Slider.Root>>;

	let { value = $bindable(), ref = $bindable(null), ...restProps }: Props = $props();
</script>

<div class="temperature-wrapper">
	<Slider.Root bind:value bind:ref {...restProps as any}>
		{#snippet children({ thumbItems, tickItems })}
			<div class="label-wrapper">
				<Label for={restProps.name}>Temperature</Label>
				<span class="value-label">{value}</span>
			</div>
			<div class="slider-wrapper">
				<span class="slider-track">
					<Slider.Range>
						{#snippet child({ props })}
							<span class="slider-range" {...props}></span>
						{/snippet}
					</Slider.Range>
				</span>
				{#each thumbItems as thumbItem, i (`thumb-${i}`)}
					<Slider.Thumb index={thumbItem.index}>
						{#snippet child({ props })}
							<span {...props} class="slider-thumb"></span>
						{/snippet}
					</Slider.Thumb>
				{/each}

				<!-- {#each tickItems as tickItem, i (`tick-${i}`)}
					<Slider.Tick index={tickItem.index} />
				{/each} -->
			</div>
		{/snippet}
	</Slider.Root>
</div>

<style>
	.temperature-wrapper {
		display: flex;
		flex-direction: column;
		gap: 6px;
		width: 180px;
	}

	.label-wrapper {
		display: flex;
		justify-content: space-between;
	}

	.value-label {
		font: var(--weight-regular) 11px / 1 var(--font-mono);
		color: var(--accent);
	}

	.slider-range {
		position: absolute;
		top: 0;
		height: 100%;
		border-radius: 2px;
		background: var(--accent);
	}

	.slider-wrapper {
		position: relative;
		height: 34px;
		display: flex;
		align-items: center;
	}

	.slider-track {
		position: relative;
		width: 100%;
		height: 4px;
		border-radius: 2px;
		background: var(--border, --bg-sunken);
		overflow: hidden;
	}

	.slider-thumb {
		width: 16px;
		height: 16px;
		border-radius: 50%;
		background: var(--white);
		border: 1px solid var(--border-strong);
		box-shadow: var(--shadow-sm);
	}
</style>
