<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Roboto&display=swap" rel="stylesheet">

<script lang="ts">
	export let name: string;
	
	import StyledTextArea from "./StyledTextArea.svelte";
	let styledTextArea;

	let mainText: string;
	mainText='Lorem Ipsum';
	
	let fontSize: number;
	fontSize=16;

	let baseline: number;
	baseline = 0;
	
	let bottomY: number;
	let baseLineY: number;
	bottomY = 0;
	baseLineY = 0;

	let styledText: string;
	styledText = '';
	
	function applyFontStyle(){
		styledTextArea.applyFontStyleModule();
		baseline = styledTextArea.getBaselineHeight();
		styledText = styledTextArea.getAppliedStyle();
	}

</script>

<main>
	<div class="mainForm">
		<h1>{name}</h1>
		<StyledTextArea bind:mainText={mainText} fontSize={fontSize} bind:this={styledTextArea} />
	</div>
	<hr>
	<div class="StyleInputs">
		<p>Style Inputs</p>
		<label for="inputFontSize">Font Size:</label>
		<input id="inputFontSize" type="text" bind:value={fontSize} on:input={applyFontStyle} />
<!--
		<label for="inputFontURL">Font URL:</label>
		<input id="inputFontURL" type="text" value={fontURL} on:change={e=>fontURL=e.target.value} />
		-->
	</div>
	<hr>
	<div class="DebugConsole">
		<p>Debug Console</p>
		<p>MainText : {mainText}</p>
		<p>FontSize : {fontSize}</p>
		<p>BaseLine : {baseline}</p>
		<p>bottomY : {bottomY}</p>
		<p>baseLineY : {baseLineY}</p>
		<p>styledText : {styledText}</p>
	</div>
</main>

<style>
	.DebugConsole {
		text-align: left;
	}
	main {
		text-align: center;
		padding: 1em;
		margin: 0 auto;
		font-family: 'Roboto', sans-serif;
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