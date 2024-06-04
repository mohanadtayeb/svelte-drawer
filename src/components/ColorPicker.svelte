<script lang="ts">
  import { createEventDispatcher } from 'svelte';
  

  export let value: string = '#ffffff';
  const dispatch = createEventDispatcher();

  function handleChange(event: Event) {
    const input = event.target as HTMLInputElement;
    value = input.value;
    dispatch('change', { color: value });
  }
</script>

  <input type="color" bind:value={value} on:input={handleChange} class=" " style="--theme-color: {value}"  />




<style>
input[type="color" i] {

}
input[type="color" i]::-webkit-color-swatch-wrapper {
  border-radius: 9999px;
  border-width: 1px;
  border-style: solid;
  border-color: var(--theme-color);
  margin-left: 10px;
  
  background-color: var(--theme-color);
}
</style>
