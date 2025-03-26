<script>
  import { Workbench, Canvas, ToolBox } from "$lib/components";
  
  let canvasRef;
  function handleExport() {
      if (canvasRef) {
          canvasRef.exportAsImage(); // Default name: canvas-export.png
          // or with custom filename:
          // canvasRef.exportAsImage('my-artwork.png');
      }
  }
</script>

<Workbench>
  
      <ToolBox slot="toolbox">
        <p>adf</p>
        <button on:click={handleExport}>Export as Image</button>
      </ToolBox>
      <Canvas 
        slot="canvas"
        bind:this={canvasRef}

        height="279mm"
        width="216mm"
        style="background-color: orange;" 
      >
            <div class="main-container">
              <div class="content-container">
                <div class="text-container">
                  <p class="title-text">Artco.</p>
                  <div class="info-container">
                    <p class="info-bolded">La Roma</p>
                    <p>Yucatan 345, La Roma, CDMX.</p>
                    <p class="info-bolded">Merida</p>
                    <p>Paseo Montejo 34, Merida Norte.</p>
                  </div>
                </div>
              </div>
            </div>
      </Canvas>
</Workbench>

<style>
  .main-container {
    position: relative;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100%;
    height: 100%;
    background-image: url("https://www.shutterstock.com/image-vector/sky-bluecloud-background-3d-white-600nw-2279761923.jpg");
    background-size: cover;
  }
  .content-container {
    width: 92%;
    height: 95%;
  }
  .text-container {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    width: 70%;
    height: 30%;
  }
  .title-text {
    font-size: 150px;
    font-weight: 800;
  }
  .info-container {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    width: 100%;
    height: 30%;
  }
  .info-bolded {
    font-weight: bold;
  }
</style>
