<script>
    import { browser } from '$app/environment';
    import { onMount, onDestroy } from 'svelte';

    /**
     * The length of the random text to generate.
     * @type {number}
     * @default 8
     */
    export let length = 8;

    /**
     * The speed (in milliseconds) at which the text updates.
     * @type {number}
     * @default 15
     */
    export let speed = 15;

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

    let requestedAnimationFrameId = null;
    let setTimeoutId = null;

    /**
     * Generates a random text string.
     * @returns {string} The generated random text.
     */
    function getRandomText() {
        let text = '';
        for (let i = 0; i < length; i++) text += characters[Math.floor(Math.random() * characters.length)];
        return text;
    }

    function animateRandomText() {
        text = getRandomText();
        
        if(!browser) return

        requestedAnimationFrameId = null;
        setTimeoutId = setTimeout(() => {
            requestedAnimationFrameId = window.requestAnimationFrame(animateRandomText);
        }, speed);
    }

    onMount(() => animateRandomText());

    onDestroy(() => {
        if(!browser) return
        window.cancelAnimationFrame(requestedAnimationFrameId);
        clearTimeout(setTimeoutId);
    });
</script>

<span style="font-family: monospace;">{text}</span>
