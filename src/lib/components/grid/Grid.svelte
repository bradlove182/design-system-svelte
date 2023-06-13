<script lang="ts">
	interface GridProps {
		gap?: 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9;
		columns?: 1 | 2 | 3 | 4 | 5;
		alignItems?: "baseline" | "center" | "end" | "start" | "stretch";
		justifyContent?: "center" | "end" | "space-between" | "start";
		flow?: "row" | "column" | "dense" | "row dense" | "column dense";
		as?: Extract<keyof HTMLElementTagNameMap, "div" | "section">;
		className?: string;
	}
	// Props
	export let as: GridProps["as"] = "div";
	export let gap: GridProps["gap"] = 0;
	export let columns: GridProps["columns"] = 1;
	export let alignItems: GridProps["alignItems"] = "stretch";
	export let justifyContent: GridProps["justifyContent"] = "start";
	export let flow: GridProps["flow"] = "row";
	export let className: GridProps["className"] = "";
</script>

<svelte:element
	this={as}
	style="
    --grid-gap: var(--spacing-{gap});
    --grid-columns: {columns};
    --align-items: {alignItems};
    --justify-content: {justifyContent};
    --grid-auto-flow: {flow};
    "
	class="grid {className}"
>
	<slot />
</svelte:element>

<style>
	.grid {
		display: grid;
		height: inherit;
		width: 100%;
		gap: var(--grid-gap, 0);
		align-items: var(--align-items, stretch);
		justify-content: var(--justify-content);
		grid-auto-flow: var(--grid-auto-flow, row);
		grid-template-columns: repeat(
			auto-fit,
			minmax(calc(100% / var(--grid-columns, 1) - var(--grid-gap)), 1fr)
		);
	}
</style>
