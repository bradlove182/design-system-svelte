<script lang="ts">
	import { createEventDispatcher } from "svelte";

	interface ButtonProps {
		as?: Extract<keyof HTMLElementTagNameMap, "button" | "span">;
		disabled?: boolean;
		variant?: "brand" | "transparent" | "outline" | "gradient";
	}

	// Events
	const dispatch = createEventDispatcher<{ click: MouseEvent }>();
	const handleClick = (event: MouseEvent) => dispatch("click", event);

	// Props
	export let as: ButtonProps["as"] = "button";
	export let disabled: ButtonProps["disabled"] = false;
	export let variant: ButtonProps["variant"] = "brand";
</script>

<svelte:element this={as} class="button {variant}" {disabled} on:click={handleClick}>
	<slot>Button</slot>
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

	.button:not(:disabled):not(.icon):hover,
	.button:not(:disabled):not(.icon):focus,
	.button:not(:disabled):not(.icon):active {
		box-shadow: var(--box-shadow-glow);
	}

	.button:disabled {
		background-color: var(--form-input-disabled);
		color: var(--text-subdued);
		cursor: not-allowed;
	}

	.brand {
		background-color: var(--brand-subdued);
		color: var(--brand);
		border-width: var(--border-1);
		border-color: var(--border-color);
	}

	.transparent {
		background-color: transparent;
	}

	.outline {
		background-color: transparent;
		border-width: var(--border-1);
		border-color: var(--border-color);
	}

	.gradient {
		background-color: var(--background);
		color: var(--text-amplified);
	}

	.gradient:after {
		content: "";
		height: 100%;
		width: 100%;
		background: var(--gradient-0);
		position: absolute;
		top: 0;
		left: 0;
		z-index: -1;
		animation: 2.7s ease-in-out 0s infinite normal both running pulsing-gradient;
	}

	.gradient:before {
		content: "";
		height: calc(100% + 2px);
		width: calc(100% + 2px);
		background-image: var(--gradient-0);
		pointer-events: none;
		border-radius: var(--border-radius-3);
		z-index: -1;
		position: absolute;
		top: -1px;
		left: -1px;
	}

	@keyframes pulsing-gradient {
		0% {
			transform: rotate(0deg);
			filter: blur(8px);
			border-radius: 5px;
		}
		33% {
			transform: rotate(-0.3deg) scale(1.03);
			filter: blur(10px);
			border-radius: 3px;
		}
		66% {
			transform: rotate(0.3deg) scale(0.99);
			filter: blur(14px);
			border-radius: 7px;
		}
		100% {
			transform: rotate(0deg);
			filter: blur(8px);
			border-radius: 5px;
		}
	}
</style>
