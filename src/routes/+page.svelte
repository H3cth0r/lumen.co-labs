<script>
  import { Workbench, Canvas, ToolBox } from "$lib/components";

</script>

<Workbench>
  
  <div slot="toolbox">
      <ToolBox />
  </div>
  <div slot="canvas">
      <Canvas 
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
  </div>
</Workbench>

<style>
  .main-container {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100%;
    height: 100%;
    background-image: url("https://i.pinimg.com/736x/44/ab/7c/44ab7cce4fede6196337b3383fa8f061.jpg");
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
