<script lang="ts">
	import { createEventDispatcher } from "svelte";

	interface ButtonIconProps {
		disabled?: boolean;
		as?: "button" | "span";
		size?: "default" | "small";
	}

	// Events
	const dispatch = createEventDispatcher<{ click: MouseEvent }>();
	const handleClick = (event: MouseEvent) => dispatch("click", event);

	// Props
	export let as: ButtonIconProps["as"] = "button";
	export let disabled: ButtonIconProps["disabled"] = false;
	export let size: ButtonIconProps["size"] = "default";
</script>

<svelte:element this={as} {disabled} class="button icon size-{size}" on:click={handleClick}>
	<slot />
</svelte:element>

<style>
	.button {
		height: 44px;
		width: max-content;
		padding: 0 var(--spacing-3);
		border-radius: var(--border-radius-3);
		display: flex;
		gap: var(--spacing-2);
		align-items: center;
		justify-content: center;
		position: relative;
		transition: box-shadow 0.3s ease;
		outline: none;
		color: var(--text-amplified);
	}

	.button:disabled {
		background-color: var(--form-input-disabled);
		color: var(--text-subdued);
		cursor: not-allowed;
	}

	.icon {
		height: 44px;
		width: 44px;
		padding: 0;
		background-color: transparent;
		border-width: 0;
	}

	.icon :global(svg) {
		height: var(--icon-size-3);
		width: var(--icon-size-3);
		color: var(--text);
		z-index: 1;
	}

	.icon:hover:not(:disabled) :global(svg),
	.icon:focus:not(:disabled) :global(svg),
	.icon:active:not(:disabled) :global(svg) {
		color: var(--brand);
	}

	.icon:hover:not(:disabled):after,
	.icon:focus:not(:disabled):after,
	.icon:active:not(:disabled):after {
		--border-hover-color: var(--brand);
		--border-thickness: 2px;
		--color: var(--brand);
		--corner: calc(var(--border-radius-3) + 2px);
		--button-background-scale: 0.92;
		box-shadow: var(--box-shadow-glow);
	}

	.icon.brand:not(:disabled):after {
		background-color: var(--foreground);
	}

	.size-small {
		height: 32px;
		width: 32px;
	}

	.icon.size-small :global(svg) {
		height: var(--icon-size-2);
		width: var(--icon-size-2);
	}

	.icon:after {
		z-index: 0;
		position: absolute;
		content: "";
		display: block;
		width: 100%;
		height: 100%;
		border-radius: var(--corner, var(--border-radius-3));
		transition: box-shadow 0.3s ease 0s, border-color 0.2s ease 0s, background 0.3s ease 0s,
			transform 0.3s cubic-bezier(0.34, 1.56, 0.64, 1) 0s;
		transform: scale(var(--button-background-scale, 1)) translateZ(0);
		border: var(--border-thickness, 1px) solid var(--border-hover-color, transparent);
		box-shadow: var(--shadow, none);
		z-index: 0;
	}
</style>
