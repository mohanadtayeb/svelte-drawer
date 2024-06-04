<script lang="ts">
  import { createEventDispatcher } from 'svelte';
  import ColorPicker from './ColorPicker.svelte';
  const dispatch = createEventDispatcher();

  export let colors: string[] = [
    '#ff0000',
    '#00ff00',
    '#0000ff',
    '#ffff00',
  ];
  
  export let palleteColor: string;
  export let background: string = '#fff';
  
  let internalColor: string = palleteColor;

  $: internalColor = palleteColor;
</script>
  
<section class="size-7 p-1 flex align-middle gap-x-0 gap-y-4 w-auto  ">
  <div class="flex flex-row gap-3 ">
    {#each colors as color}
      <button on:click={() => {
        dispatch('color', { color });
        palleteColor = color;
        internalColor = color;
        
      }}
      
      >
        <span class="visually-hidden ">
          Select the color {color}
        </span>
        <div style="background: {color};" class="w-5 h-5 "></div>
      </button>
    {/each}
  </div>
    
    <ColorPicker value={internalColor} on:change={(event) => {
      palleteColor = event.detail.color;
      internalColor = event.detail.color;
    }} />



  <button
    on:click={() => {
      dispatch('color', { color: background });
      palleteColor = background;
    }}
  >
    <span class="visually-hidden ">
      Select the background color to clear the canvas
    </span>
    <div style="width: 20px; height: 20px; background: {background};" class="ml-20 p-0"></div>
  </button>
  <svg style="color: {palleteColor}" viewBox="-50 -50 100 100" class="flex-shrink-0"></svg>
</section>
  
