<script lang="ts">
	import { DropdownMenu } from 'bits-ui';
	import Label from './Label.svelte';
</script>

<div class="dropdown-wrapper">
	<DropdownMenu.Root>
		<Label for="corpus-menu">Corpus</Label>
		<DropdownMenu.Trigger id="corpus-menu">
			{#snippet child({ props })}
				<button {...props} class="trigger">
					<span class="dot"></span>
					<span class="trigger-text">No corpus</span>
					<span class="dropdown-triangle">&#9660;</span>
				</button>
			{/snippet}
		</DropdownMenu.Trigger>
	</DropdownMenu.Root>
</div>

<style>
	.dropdown-wrapper {
		position: relative;
		display: flex;
		flex-direction: column;
		gap: 6px;
		min-width: 230px;
	}

	.dot {
		width: 7px;
		height: 7px;
		border-radius: 50%;
		background: var(--warm-300);
	}

	.trigger {
		display: flex;
		align-items: center;
		gap: 10px;
		padding: 8px 12px;
		border: 1px solid var(--accent);
		border-radius: var(--radius-md);
		background: var(--white);
		outline: none;
	}

	.trigger:focus {
		box-shadow: var(--shadow-focus);
	}

	.trigger-text {
		font: var(--type-body-sm);
		color: var(--fg-muted);
	}

	.dropdown-triangle {
		margin-left: auto;
		font: var(--type-caption);
		color: var(--accent);
	}

	.trigger[data-state='open'] .dropdown-triangle {
		transform: rotate(180deg);
	}
</style>
