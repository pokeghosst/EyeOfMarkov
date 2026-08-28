<script lang="ts">
	import { RadioGroup, type WithoutChildrenOrChild, useId } from 'bits-ui';
	import Label from './Label.svelte';

	type Item = {
		value: string;
		label: string;
		disabled?: boolean;
	};

	type Props = WithoutChildrenOrChild<RadioGroup.RootProps> & {
		items: Item[];
	};

	let { value = $bindable(''), ref = $bindable(null), items, ...restProps }: Props = $props();
</script>

<RadioGroup.Root bind:value bind:ref {...restProps}>
	<Label for={restProps.name}>N-value</Label>
	<div class="radio-wrapper">
		{#each items as item, i (`item-${i}`)}
			{@const id = useId()}
			<div class="radio-item">
				<RadioGroup.Item {id} value={item.value} disabled={item.disabled}>
					{#snippet child({ props })}
						<button {...props}>{item.label}</button>
					{/snippet}
				</RadioGroup.Item>
				<!-- <RadioLabel.Root for={id}>{item.label}</RadioLabel.Root> -->
			</div>
		{/each}
	</div>
</RadioGroup.Root>

<style>
	.radio-wrapper {
		display: flex;
		gap: 4px;
	}

	.radio-item button {
		width: 34px;
		height: 34px;
		border: 1px solid var(--border);
		border-radius: var(--radius-md);
		background: var(--white);
		font: var(--weight-regular) 13px / 1 var(--font-mono);
		color: var(--fg-muted);
		cursor: pointer;
	}

	.radio-item button[data-state='checked'] {
		border: 1px solid var(--accent) hsl(350, 73%, 29%);
		background: var(--accent);
		color: rgb(255, 255, 255);
	}
</style>
