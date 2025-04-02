<script>
  import { onMount, afterUpdate } from 'svelte';

  export let width = '100%';
  export let height = '100%';
  export let x = 0;
  export let y = 0;

  let container;
  let imgElement;

  const updatePosition = () => {
    if (!container || !imgElement) return;

    // Container dimensions
    const containerRect = container.getBoundingClientRect();
    const containerWidth = containerRect.width;
    const containerHeight = containerRect.height;

    // Natural image dimensions
    const naturalWidth = imgElement.naturalWidth;
    const naturalHeight = imgElement.naturalHeight;

    if (naturalWidth === 0 || naturalHeight === 0) return;

    // Calculate scale to cover container
    const scale = Math.max(
      containerWidth / naturalWidth,
      containerHeight / naturalHeight
    );

    // Calculate scaled coordinates
    const scaledX = x * scale;
    const scaledY = y * scale;

    // Calculate translation to center the scaled coordinates
    const translateX = containerWidth / 2 - scaledX;
    const translateY = containerHeight / 2 - scaledY;

    // Apply the transformation to the image
    imgElement.style.transform = `translate(${translateX}px, ${translateY}px) scale(${scale})`;
  };

  const handleImageLoad = () => {
    updatePosition();
  };

  onMount(() => {
    imgElement = container.querySelector('img');
    if (imgElement) {
      imgElement.addEventListener('load', handleImageLoad);
      if (imgElement.complete) handleImageLoad();
    }
  });

  afterUpdate(updatePosition);
</script>

<div class="container" bind:this={container} style="width: {width}; height: {height};">
  <div class="image-wrapper">
    <slot />
  </div>
</div>

<style>
  .container {
    position: relative;
    overflow: hidden;
    background-color: red;
  }

  .image-wrapper {
    position: absolute;
    width: 100%;
    height: 100%;
    overflow: hidden;
  }

  .image-wrapper img {
    position: absolute;
    width: auto;
    height: auto;
    max-width: none;
    transform-origin: 0 0;
    will-change: transform;
  }
</style>
