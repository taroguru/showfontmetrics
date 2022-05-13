<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Roboto&display=swap" rel="stylesheet">

<script lang="ts">
	import {onMount} from 'svelte';
	import {tick} from 'svelte'; 

	//Default Properties
	export let name: string;
	
	//Elements
	import StyledTextArea from "./StyledTextArea.svelte";
	let styledTextArea: StyledTextArea;
	let baselineElement: SVGSVGElement;

	let leftElement: SVGSVGElement;
	let rightElement: SVGSVGElement;
	let bottomElement: SVGSVGElement;
	let topElement: SVGSVGElement;

	//Properties
	let mainText: string;
	mainText='興 À, É, È, Ç Lorem Ipsum 한글뙜따!?A';
	
	//스타일 관련 텍스트
	let fontSize: number	= 14;
	let lineHeight: string	= 'normal';
	let styledText: string	= "";
	let fontHeight: number  = 14;
	let ascent: number		= 0;
	let descent: number		= 0;
	
	
	async function applyFontStyle(){
		styledTextArea.applyFontStyleModule();
		styledText=styledTextArea.getAppliedStyle();
		drawRectGuideLine();
	}

	async function drawRectGuideLine(){
		boundRect = toString(styledTextArea.getSpanElement().getBoundingClientRect());
		await tick();	//화면 갱신을 기다리자.
		positionLine();
	}

	function positionLine(){
		
		//가이드라인을 갱신
		topElement.style.top 	= styledTextArea.getSpanElement().getBoundingClientRect().top + "px" ;
		bottomElement.style.top = styledTextArea.getSpanElement().getBoundingClientRect().bottom + "px" ;
		leftElement.style.left 	= styledTextArea.getSpanElement().getBoundingClientRect().left + "px" ;
		rightElement.style.left = styledTextArea.getSpanElement().getBoundingClientRect().right + "px" ;

		let baseilneHeight = styledTextArea.getBaselineHeight();
		let newLinePos = styledTextArea.getSpanElement().getBoundingClientRect().bottom -  baseilneHeight;
		baselineElement.style.top = newLinePos + "px" ;

		fontHeight = styledTextArea.getSpanElement().getBoundingClientRect().bottom - styledTextArea.getSpanElement().getBoundingClientRect().top;
		ascent = fontHeight - baseilneHeight;
		descent = baseilneHeight;
		
	}
	let boundRect: string = '';

	function toString(rect: DOMRect): string{
		let para: string ='';
		for (var key in rect) {
			if(typeof rect[key] !== 'function') {
				para += `${ key } : ${ rect[key] } `;
			}
		}

		return para;
	}

	onMount(async() => {
		applyFontStyle();
	});
	
</script>

<svg class="lineHorizontal" bind:this={baselineElement}>
	<line x1="0" y1="0" x2="100%" y2="0" style="stroke:rgb(255,0,0);stroke-width:1"></line>
</svg> 
<svg class="lineHorizontal" bind:this={bottomElement}>
	<line x1="0" y1="0" x2="100%" y2="0" style="stroke:rgb(255,0,0);stroke-width:1"></line>
</svg> 
<svg class="lineHorizontal" bind:this={topElement}>
	<line x1="0" y1="0" x2="100%" y2="0" style="stroke:rgb(255,0,0);stroke-width:1"></line>
</svg> 
<svg class="lineVertical" bind:this={leftElement}>
	<line x1="0" y1="0" x2="0" y2="100%" style="stroke:rgb(255,0,0);stroke-width:1"></line>
</svg> 
<svg class="lineVertical" bind:this={rightElement}>
	<line x1="0" y1="0" x2="0" y2="100%" style="stroke:rgb(255,0,0);stroke-width:1"></line>
</svg> 

<main>
	<div class="mainForm">
		<h1>{name}</h1>
		<StyledTextArea bind:mainText={mainText} fontSize={fontSize} lineHeight={lineHeight} appliedStyle={styledText} bind:this={styledTextArea} />
	</div>
	<hr>
	<div class="StyleInputs">
		<p>Style Text. Edit below!</p>
		<textarea id="StyleTextArea" bind:value={styledText} on:input={drawRectGuideLine}/> 
		<!-- not sued items-->
		<div hidden>
			<label for="inputFontSize">Font Size(pixel) : Not Use!</label>
			<input id="inputFontSize" type="text" bind:value={fontSize} on:input={applyFontStyle} />
		
			<label for="inputLineHeight">line-height : Not Use! </label>
			<input id="inputLineHeight" type="text" bind:value={lineHeight} on:change={applyFontStyle} />
		</div>
<!--
		<label for="inputFontURL">Font URL:</label>
		<input id="inputFontURL" type="text" value={fontURL} on:change={e=>fontURL=e.target.value} />
		-->
	</div>
	<hr>
	<div class="DebugConsole">
		<p>FontMetrics Infomation : </p>
		<ul>
			<li><p>BoundRect: {boundRect}</p></li>
			<li><p>MainText : {mainText}</p></li>
			<li><p>FontHeight : {fontHeight}px</p></li>
			<li><p>Ascent : {ascent}px</p></li>
			<li><p>Dscent : {descent}px</p></li>
		</ul>
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

	.lineVertical{
		position:absolute;
		top : 0 ;
		height:100%;
		width:1px;
	}

	.lineHorizontal{
		position:absolute;
		left : 0 ;
		height:1px;
		width:100%
	}

	#StyleTextArea {
		height:100px;
		width:80%;
	}
</style>