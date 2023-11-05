
# Corrupted Svelte

Corrupted Svelte is a highly efficient and lightweight component library designed for creating visually intriguing, corrupted-style websites using the Svelte framework.

## Demo
Check out the live demo to see Corrupted Svelte's components in action: [Corrupted Svelte Demo](https://svelte.dev/repl/ad7bb4fb7cbf431683fe394f88cf83a6?version=4.2.2)

## Installation

You can install Corrupted Svelte using npm or pnpm. Here are the commands for both package managers:

```bash
npm install corrupted-svelte --save-dev
pnpm install corrupted-svelte --save-dev
```

## How to Use

Corrupted Svelte offers a range of components to add captivating visual effects to your Svelte applications. Here's how to use some of the available components:

### Corrupted Text
Make text look like the Minecraft enchantment table ✨

```svelte
<script>
    import CorruptedText from 'corrupted-svelte/CorruptedText';
</script>

<CorruptedText />
<CorruptedText length="100" />
<CorruptedText speed="1000" />
<CorruptedText characters="€¥£$">
```

![30FPS GIF](https://github.com/UltraCakeBakery/corrupted-text-svelte/assets/12383587/079a12de-33ec-42cf-bd04-c6c6c2290d9f)

### Flicker
Make components flicker, creating a strobe-like effect 🌟

```svelte
<script>
    import Flicker from 'corrupted-svelte/Flicker';
</script>

<Flicker>Look at me flickering!</Flicker>
<Flicker speed="1">I'm flickering slower</Flicker>
<Flicker speed="3">I look like a lightbulb that needs replacing!</Flicker>
```

### Static Noise
Create static noise backgrounds as if you forgot to plug the cable into an old TV or have a bad signal 📺

```svelte
<script>
    import StaticNoise from 'corrupted-svelte/StaticNoise';
</script>

<header style="width: 100%; height: 80vh;">
    <StaticNoise />
</header>
```

If you find this library useful, please consider leaving a like or a star on the repository. Your support is greatly appreciated! ❤️