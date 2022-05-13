<script lang="ts">
     
    export let mainText: string;
    export let fontSize: number;
    export let lineHeight: string;
    let textAreaElement: Element;
    export let appliedStyle: string;
    let spanElement: Element;
    export function setFontFamily(newFontFamily: string) {
        //this.fontfamily = newFontFamily;
        textAreaElement.style.fontFamily = newFontFamily;
        spanElement.style.fontFamily = newFontFamily;
    }

    export function getSpanElement(): Element{
        return spanElement;
    }

    export function getAppliedStyle(): string{
        return appliedStyle;
    }

    export function getTextAreaElement(): Element{
        return textAreaElement;
    }

	export function applyFontStyleModule(){
		appliedStyle=`font-size: ${fontSize}px;
line-height: ${lineHeight};
letter-spacing: 0px;
word-spacing: 0px;
font-family: CustomFontFamily;`;
	}

    export function setAppliedStyle(style: string) {
        appliedStyle = style;
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


</script>
<div >
    <textarea bind:value={mainText} bind:this={textAreaElement} />
    <br />
    <span id="lorem" style={appliedStyle} bind:this={spanElement}>{mainText}</span>
</div>
    
<style>
	textarea{
		width: 80%;
		height: 3rem;
	}

    #lorem{
        background-color: lightblue;
    }
</style>
