<script>
	import { Button, Grid, ButtonIcon } from "$lib";
</script>

<Grid gap={2}>
	<Button variant="gradient" on:click={(event) => console.log(event)} />
	<ButtonIcon variant="gradient" on:click={(event) => console.log(event)} />
</Grid>
