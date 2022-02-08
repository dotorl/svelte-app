<script>
	export let name;
	name = 'choks';

	function assign() {
		name = 'asdfasfd';
	}
</script>

<main>
	<h1>Hello {name}!</h1>
	<p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p>
</main>

<button on:click={assign}>assign</button>

<!-- 단방향 바인딩 -->
<!-- <input type="text" value={name} on:input={e => (name = e.target.value)} /> -->

<!-- 양방향 바인딩 -->
<input type="text" bind:value={name} />



<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>