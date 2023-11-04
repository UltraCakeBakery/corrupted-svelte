<script>
    import { onMount } from 'svelte';

    /**
     * The length of the random text to generate.
     * @type {number | string}
     * @default 8
     */
    export let length = 8;
    $: lengthAsNumber = Number(length)
    
    /**
     * The speed (in milliseconds) at which the text updates.
     * @type {number | string}
     * @default 15
     */
    export let speed = 15;
    $: speedAsNumber = Number(speed)

    /**
     * The characters to use for generating random text.
     * @type {string}
     * @default 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789#@!$%&*)('
     */
    export let characters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789#@!$%&*)(';

    /**
     * The initial text to be displayed (random string by default).
     * @type {string}
     */
    export let text = getRandomText();

    /** @type {number | null} */
    let requestedAnimationFrameId = null;
    /** @type {number | null} */
    let setTimeoutId = null;

    /**
     * Generates a random text string.
     * @returns {string} The generated random text.
     */
    function getRandomText() {
        let text = '';
        for (let i = 0; i < lengthAsNumber; i++) text += characters[Math.floor(Math.random() * characters.length)];
        return text;
    }

    function animateRandomText() {
        text = getRandomText();
        
        requestedAnimationFrameId = null;
        setTimeoutId = setTimeout(() => {
            requestedAnimationFrameId = window.requestAnimationFrame(animateRandomText);
        }, speedAsNumber);
    }

    onMount(() => {
        animateRandomText()
        return () => {
            if(requestedAnimationFrameId) window.cancelAnimationFrame(requestedAnimationFrameId);
            if(setTimeoutId) clearTimeout(setTimeoutId);
        }
    });
</script>

<span style="font-family: monospace;" class={$$props.class}>{text}</span>
