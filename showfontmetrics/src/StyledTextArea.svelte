<script lang="ts">
     
    export let mainText: string;
    export let fontSize: number;
    let textAreaElement: Element;
    let appliedStyle: string;
    let spanElement: Element;

    export function getSpanElement(): Element{
        return spanElement;
    }

    export function getAppliedStyle(): string{
        return appliedStyle;
    }

	export function applyFontStyleModule(){
		appliedStyle=`
			font-size: ${fontSize}px;
		`;
	}

    export function getBaselineHeight(): number {
        let bottomY = spanElement.getBoundingClientRect().bottom;//viewport pos of bottom of el
        
        let baselineLocator = document.createElement("img"); // needs to be an inline element without a baseline (so its bottom (not baseline) is used for alignment)
        spanElement.appendChild(baselineLocator);
        
        baselineLocator.style.verticalAlign = 'baseline' ; // aligns bottom of baselineLocator with baseline of el
        let baseLineY = baselineLocator.getBoundingClientRect().bottom;//viewport pos of baseline
        spanElement.removeChild(baselineLocator);
            
        return (bottomY - baseLineY) ;        
    }

    export function getTextAreaElement(): Element{
        return textAreaElement;
    }

    export function getBottomY(element: Element): number{
        return element.getBoundingClientRect().bottom;
    }

    export function getTopY(element: Element): number{
        return element.getBoundingClientRect().top;
    }

    export function getLeftX(element: Element): number{
        return element.getBoundingClientRect().left;
    }

    export function getRightX(element: Element): number{
        return element.getBoundingClientRect().right;
    }

</script>

<textarea bind:value={mainText} bind:this={textAreaElement} />
<br />
<span id="lorem" style={appliedStyle} bind:this={spanElement}>{mainText}</span>
    
<style>
	textarea{
		width: 80%;
		height: 50px;
	}

    #lorem{
        background-color: lightblue;
    }
</style>
