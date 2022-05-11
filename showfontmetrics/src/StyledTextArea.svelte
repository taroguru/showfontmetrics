<script lang="ts">
     
    export let mainText: string;
    export let fontSize: number;
    let textAreaElement: Element;
    let appliedStyle: string;

    export function getAppliedStyle(): string{
        return appliedStyle;
    }

	export function applyFontStyleModule(){
		appliedStyle=`
			font-size: ${fontSize}px;
		`;
	}

    export function getBaselineHeight(): number {
        let bottomY = textAreaElement.getBoundingClientRect().bottom;//viewport pos of bottom of el
        
        let baselineLocator = document.createElement("img"); // needs to be an inline element without a baseline (so its bottom (not baseline) is used for alignment)
        textAreaElement.appendChild(baselineLocator);

        baselineLocator.style.verticalAlign = 'baseline' ; // aligns bottom of baselineLocator with baseline of el
        let baseLineY = baselineLocator.getBoundingClientRect().bottom;//viewport pos of baseline
        textAreaElement.removeChild(baselineLocator);
            
        return (bottomY - baseLineY) ;        
    }

    export function getTextAreaElement(): Element{
        return textAreaElement;
    }


</script>

<textarea bind:value={mainText} style={appliedStyle} bind:this={textAreaElement} />

<style>
	textarea{
		width: 80%;
		height: 200px;
	}
</style>
