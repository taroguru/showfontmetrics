<script lang="ts">
     
    export let mainText: string;
    export let fontSize: number;
    
    let appliedStyle: string;

	export function applyFontStyleModule(){
		appliedStyle=`
			font-size: ${fontSize}px;
		`;
	}

</script>

<textarea bind:value={mainText} style={appliedStyle} />

<style>
	textarea{
		width: 80%;
		height: 200px;
	}
</style>
