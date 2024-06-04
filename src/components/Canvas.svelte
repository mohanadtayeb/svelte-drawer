<script lang="ts">
	
import {onMount} from 'svelte';

export let width: number = 800;
export let height: number = 600;
export let color: string = '#333';
export let background: string = '#fff';
    
    let canvas: HTMLCanvasElement | null, context: CanvasRenderingContext2D, isDrawing: boolean, start: object, t: number, l: number;


    onMount(()=> {
        context = canvas?.getContext('2d')!;
        context.lineWidth = 5;

        handleSize();
    })

    $: if(context){
        context.strokeStyle = color;
    }

    const handleStart = (({offsetX : x, offsetY : y}: {offsetX: number, offsetY: number}) => {
        if (color == background){
            context.clearRect(0, 0, width, height);
            
        } else {
            isDrawing = true;
            start = {x, y};
        }

    })

    const handleEnd = () => { isDrawing = false; }
    const handleMove = (({offsetX: x1, offsetY: y1}: {offsetX: number, offsetY: number}) => {
		if(!isDrawing) return

        const { x, y } = start as { x: number, y: number };
		context.beginPath()
		context.moveTo(x, y)
		context.lineTo(x1, y1)
		context.closePath()
		context.stroke()
		
		start = { x: x1, y: y1 }
    })

    const handleSize = () => {
        const {top, left} = canvas?.getBoundingClientRect()!;
        t = top;
        l = left;
    }

</script>

<svelte:window on:resize={handleSize} />


<canvas
{width}
				{height}
				style:background
				bind:this={canvas} 
				on:mousedown={handleStart}	
				on:touchstart={e => {
					const { clientX, clientY } = e.touches[0]
					handleStart({
						offsetX: clientX - l,
						offsetY: clientY - t
					})
				}}	
				on:mouseup={handleEnd}				
				on:touchend={handleEnd}				
				on:mouseleave={handleEnd}
				on:mousemove={handleMove}
				on:touchmove={e => {
					const { clientX, clientY } = e.touches[0]
					handleMove({
						offsetX: clientX - l,
						offsetY: clientY - t
					})
				}}
				style="border: 3px solid {color};"
/>
