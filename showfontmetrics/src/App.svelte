<script lang="ts">

	let mainText: string;
	mainText='Lorem Ipsum';

	function InputHandler (event: Event) {
		mainText = event.target.value;
	}
</script>
 
<main>
	<h1>Show me the FontMetrics</h1>
	<textarea  value={mainText} on:input={InputHandler} />
	<div>Debug Console : <br />{mainText}</div>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
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