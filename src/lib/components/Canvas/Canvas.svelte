<script>
  export let width = "100%";
  export let height = "100%";
  export let style = "";
</script>

<div class="canvas-container" style="width: {width}; height: {height}; {style}">
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
