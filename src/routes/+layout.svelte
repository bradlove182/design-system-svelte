<script lang="ts">
	import type { LayoutData } from './$types.d.ts';

	export let data: LayoutData;
</script>

<slot>{ data }</slot>

<style>
    @import "$lib/index.css";
</style>
