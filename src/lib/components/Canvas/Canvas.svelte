<script>
    import html2canvas from 'html2canvas';
    
    export let width = "100%";
    export let height = "100%";
    export let style = "";
    
    let canvasContainer;

    export async function exportAsImage(filename = "canvas-export.png") {
        if (!canvasContainer) return;

        try {
            const canvas = await html2canvas(canvasContainer, {
                scale: 2,
                useCORS: true, // Enable CORS
                allowTaint: true, // Allow cross-origin images
                logging: true,
                backgroundColor: null // Maintain transparency
            });
            
            const dataUrl = canvas.toDataURL('image/png');
            const link = document.createElement('a');
            link.download = filename;
            link.href = dataUrl;
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
        } catch (error) {
            console.error('Error exporting:', error);
        }
    }
</script>

<div class="canvas-container" bind:this={canvasContainer} style="width: {width}; height: {height}; {style}">
    <slot/>
</div>

<style>
    .canvas-container {
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
    }
</style>
