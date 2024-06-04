<script lang="ts">
  import Canvas from './components/Canvas.svelte';
  import Pallete from './components/Pallete.svelte';
  import './app.css'

  const colors: string[] = [
    '#d58141',
    '#d7c44c',
    '#4fa9cc',
    '#3f8d27',
  ];
  const background: string = '#fff';

  let color: string = colors[0];
  $: console.log(color)
</script>

<main>
  <Canvas {color} {background} />




  <div class="border-solid border-2 border-black rounded-full p-2">
  <Pallete {colors} bind:palleteColor={color} {background} />
</div>
</main>

<style>
  :global(body) {
    margin: 0;
    padding: 0;
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    background: #e5e5e5;
  }
  
  :global(.visually-hidden:not(:focus):not(:active)) {
    clip: rect(0 0 0 0);
    clip-path: inset(50%);
    height: 1px;
    width: 1px;
    overflow: hidden;
    position: absolute;
    white-space: nowrap;
  }
  
  main {
    max-width: 300px;
    display: flex;
    flex-direction: column;
    gap: 0.5rem 0;
  }
  
  main :global(canvas) {
    align-self: center;
  }
</style>
