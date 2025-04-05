<script>
  import { onMount } from 'svelte';

  let container; // Reference to the container div
  let imgElement; // Reference to the image element

  onMount(() => {
    if (container) {
      // Find the first image in the slot content
      imgElement = container.querySelector('img');
      
      if (imgElement) {
        // Check if image is already loaded
        if (imgElement.complete) {
          logImageSize();
        } else {
          // Wait for image to load
          imgElement.addEventListener('load', logImageSize);
        }
      }
    }
  });

  function logImageSize() {
    if (imgElement) {
      console.log('Image dimensions:', {
        width: imgElement.naturalWidth,
        height: imgElement.naturalHeight
      });
    }
    // Cleanup event listener
    imgElement?.removeEventListener('load', logImageSize);
  }
</script>

<div class="img-container" bind:this={container}>
  <slot></slot>
</div>
