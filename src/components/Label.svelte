<script lang="ts">
	import { Label } from 'bits-ui';
	import type { Snippet } from 'svelte';

	type Props = Label.RootProps & { children: Snippet };

	let { children, ...restProps }: Props = $props();
</script>

<Label.Root {...restProps}>
	{#snippet child({ props })}
		<label {...props} class="label">{@render children()}</label>
	{/snippet}
</Label.Root>

<style>
	.label {
		font: var(--type-overline);
		letter-spacing: var(--tracking-widest);
		text-transform: uppercase;
		color: var(--fg-muted);
	}
</style>
