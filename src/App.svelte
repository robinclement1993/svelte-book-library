<script>
	import { Route, Router } from "svelte-routing";
	import Library from "./Library/Library.svelte";
	import Detail from "./Library/Detail.svelte";
	import Create from "./Library/Create.svelte";

	export let url = "";
</script>

<Router {url}>
	<main>
		<Route path="/create">
			<Create />
		</Route>
		<Route path="/books/:id" let:params>
			<Detail id={params.id} />
		</Route>
		<Route path="">
			<Library />
		</Route>
	</main>
</Router>

<style>
	main {
		padding: var(--spacingLarge);
	}
</style>
