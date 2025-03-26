<script>
    import html2canvas from 'html2canvas';
    
    export let width = "100%";
    export let height = "100%";
    export let style = "";
    
    let canvasContainer;

    function parseDimension(dimension) {
        const match = dimension.match(/^([\d.]+)(mm|px|%)$/);
        return match ? { value: parseFloat(match[1]), unit: match[2] } : null;
    }

    export async function exportAsImage(filename = "canvas-export.png") {
        if (!canvasContainer) return;

        try {
            const widthDim = parseDimension(width);
            const heightDim = parseDimension(height);

            if (!widthDim || !heightDim || widthDim.unit !== 'mm' || heightDim.unit !== 'mm') {
                console.error('Width and height must be in mm for accurate export.');
                return;
            }

            const targetDPI = 300; // Adjust target DPI as needed (e.g., 300 for print quality)
            const desiredWidthPx = (widthDim.value / 25.4) * targetDPI;
            const desiredHeightPx = (heightDim.value / 25.4) * targetDPI;

            const actualWidthPx = canvasContainer.offsetWidth;
            const actualHeightPx = canvasContainer.offsetHeight;

            const scaleX = desiredWidthPx / actualWidthPx;
            const scaleY = desiredHeightPx / actualHeightPx;
            const scale = Math.max(scaleX, scaleY);

            const canvas = await html2canvas(canvasContainer, {
                scale: scale,
                useCORS: true,
                allowTaint: true,
                logging: true,
                backgroundColor: null
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
