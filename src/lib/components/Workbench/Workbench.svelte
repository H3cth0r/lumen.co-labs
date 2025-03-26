<script>
</script>

<div class="workbench-container {$$slots.toolbox ? 'with-toolbox' : ''}">
  {#if $$slots.toolbox}
    <div class="toolbox-area">
      <slot name="toolbox" />
    </div>
  {/if}
  <div class="main-area">
    <slot name="canvas" />
  </div>
</div>

<style>
  .workbench-container {
    display: grid;
    grid-template-columns: 1fr;
    min-width: 100vw;
    min-height: 100vh;
    background-color: black;
  }

  .with-toolbox {
    grid-template-columns: 250px 1fr;
  }

  .toolbox-area {
    background-color: #333;
  }
  .main-area {
    position: relative;
    overflow: hidden;
  }
</style>
