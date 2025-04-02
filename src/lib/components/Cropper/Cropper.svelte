<script>
  export let width = "200px";
  export let height = "200px";
  export let centerX = 0;
  export let centerY = 0;

  let container;
  let slottedImage;
  let imageLoaded = false;

  // Convert dimension strings to numbers (removing 'px', '%', etc.)
  const getNumericValue = (value) => {
    if (typeof value === 'number') return value;
    return parseInt(value, 10) || 0;
  };

  const widthValue = getNumericValue(width);
  const heightValue = getNumericValue(height);

  // Position the image when it loads
  function handleImageLoad() {
    if (!slottedImage) return;
    
    const imgWidth = slottedImage.naturalWidth;
    const imgHeight = slottedImage.naturalHeight;
    
    // Calculate position to center the specified coordinates in the viewport
    const left = -(centerX - widthValue / 2);
    const top = -(centerY - heightValue / 2);
    
    // Apply positioning
    slottedImage.style.position = "absolute";
    slottedImage.style.left = left + "px";
    slottedImage.style.top = top + "px";
    
    imageLoaded = true;
  }

  // Function to find the img element in the slot
  function setupImage() {
    if (!container) return;
    
    // Find the slotted image
    slottedImage = container.querySelector("img");
    
    if (slottedImage) {
      if (slottedImage.complete) {
        handleImageLoad();
      } else {
        slottedImage.onload = handleImageLoad;
      }
    }
  }

  $: if (container && !imageLoaded) {
    setupImage();
  }

  $: if (imageLoaded && slottedImage) {
    // Update positioning when centerX or centerY changes
    const left = -(centerX - widthValue / 2);
    const top = -(centerY - heightValue / 2);
    slottedImage.style.left = left + "px";
    slottedImage.style.top = top + "px";
  }
</script>

<div 
  bind:this={container}
  class="cropper-container"
  style="width: {width}; height: {height}; position: relative; overflow: hidden;"
>
  <slot></slot>
</div>

<style>
  .cropper-container {
    display: inline-block;
    background-color: red;
  }
</style>
