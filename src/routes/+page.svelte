<script lang="ts">
	import Database from "@tauri-apps/plugin-sql";

	async function getTables() {
		const db = await Database.load("test.db");
		// get all tables

		await db
			.execute("SELECT * FROM sqlite_master WHERE type='table';")
			.then((result) => {
				return result;
			})
			.catch((err) => {
				return err;
			});
	}
</script>

<h1>Welcome to SvelteKit</h1>

<div id="tables">
	{#await getTables()}
		<p>Loading...</p>
	{:then tables}
		{#each tables as table}
			<p>{table.name}</p>
		{/each}
	{:catch error}
		<p>{error}</p>
	{/await}
</div>
