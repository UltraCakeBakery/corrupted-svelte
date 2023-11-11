<script>
    import CorruptedText from "$lib/CorruptedText.svelte";
    import ColorGlitch from "$lib/ColorGlitch.svelte";
    import StaticNoise from "$lib/StaticNoise.svelte";
    import Flicker from "$lib/Flicker.svelte";
</script>

<header>
    <StaticNoise class="absolute" darkness={220}/>
    <div class="">
        <h1>Corrupted Svelte</h1>
        Amazing, lightweight, high performance components for Svelte for quickly adding corrupted effects to your website.<br/><br/>
        Made by <CorruptedText length={37}></CorruptedText>
    </div>
</header>

<Flicker>
    <div style="height: 200vh; padding: 20rem;">
        <div style="width: 200px; height: 200px; background-color: red;">
            HALLO
        </div>
    </div>
</Flicker>

<style>
    :global(html, body) {
        padding: 0px;
        margin: 0px;
    }

    :global(.absolute) {
        position: absolute;
    }

    header {
        position: relative; 
        display: flex; 
        justify-content: center; 
        align-items: center;
        height: 100vh;
        width: 100%;
        background: #222;
    }
</style>