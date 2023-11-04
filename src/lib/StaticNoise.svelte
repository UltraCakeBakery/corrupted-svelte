<script>
    import { onMount } from 'svelte';

    /**
   * @type {HTMLCanvasElement | null}
   */
    let canvas = null
    $: canvasContext2D = canvas?.getContext('2d') ?? null

    /**
     * The amount of frames to prerender for better performance
     * @type {number | string}
     * @default 8
     */
    export let frames = 32;
    $: framesAsNumber = Number(frames)
    $: preparedFrames = new Array(framesAsNumber).fill(null).map(_ => generateFrame(canvasContext2D))
    
    /**
     * The speed (in milliseconds) at which the text updates. Set to 0 for no framerate limit 
     * @type {number | string}
     */
    export let speed = 0;
    $: speedAsNumber = Number(speed)
    
	
    /**
     * How black the darkness pixel is.
     * @type {number | string} - a number between 0 and 255
     */
    export let darkness = 220;
    $: darknessAsNumber = Number(darkness)

    /** @type {number | null} */
    let requestedAnimationFrameId = null;
    /** @type {number | null} */
    let setTimeoutId = null;


    /**
   * Generates a random frame for alter re-use.
   * @returns {?idata} The generated frame.
   * @param {CanvasRenderingContext2D | null} canvasContext2D
   */
    function generateFrame(canvasContext2D) {
        if(!canvas || !canvasContext2D) return null
        const idata = canvasContext2D.createImageData(canvas.parentNode.offsetWidth, canvas.parentNode.offsetHeight);
        const buffer32 = new Uint32Array(idata.data.buffer);
	
	    for(let i = 0; i < buffer32.length; i++) buffer32[i] = ((Math.random() * darknessAsNumber)|0) << 24;

        return idata
    }
	
    function animateRandomText() {
        const randomFrame = preparedFrames[Math.floor(Math.random() * preparedFrames.length)];
        if (randomFrame && canvasContext2D) canvasContext2D.putImageData(randomFrame, 0, 0, );
			
        requestedAnimationFrameId = null;
        setTimeoutId = setTimeout(() => {
            requestedAnimationFrameId = window.requestAnimationFrame(animateRandomText);
        }, speedAsNumber);
    }

    function resize()
    {
        if(!canvas) return
        // @ts-ignore
        canvas.width = canvas.parentNode?.offsetWidth ?? canvas.offsetWidth
        // @ts-ignore
        canvas.height = canvas.parentNode?.offsetHeight ?? canvas.offsetWidth
        canvas = canvas
    }

    onMount(() => {
        resize()
        animateRandomText()

        return () => {
            if(requestedAnimationFrameId) window.cancelAnimationFrame(requestedAnimationFrameId);
            if(setTimeoutId) clearTimeout(setTimeoutId);
        }
    });
</script>

<svelte:window on:resize={resize}></svelte:window>

<canvas bind:this={canvas} class={$$props.class}></canvas>