<script>
  // SECTIONS
  import TextOnly from "./TextOnly.svelte";
  import ImagesOnly from "./ImagesOnly.svelte";
  import OnomatopoeiaOnly from "./OnomatopoeiaOnly.svelte";
  import WordsAndImages from "./WordsAndImages.svelte";
  import WordsAndImagesAndOnomatopoeia from "./WordsAndImagesAndOnomatopoeia.svelte";

  // PLACEHOLDER
  import Text from "./Text.svelte";
</script>

<style>
  body,
  html {
    background: black;
    color: white;
    font-family: Helvetica, sans-serif;
    margin: 0;
  }

  main {
    background: black;
    width: 100vw;
  }

  h1 {
    text-align: center;
    font-family: monospace;
    background: darkgrey;
    display: block;
    margin-left: auto;
    margin-right: auto;
    padding: 20px;
    color: red;
    font-size: 24px;
    letter-spacing: 2px;
    font-weight: normal;
  }
</style>

<main>
  <WordsAndImages />
  <h1>Section above: Words + Faces</h1>
  <Text />
  <WordsAndImagesAndOnomatopoeia />
  <h1>Section above: Words + Faces + Onomatopoeia</h1>
  <Text />
  <ImagesOnly />
  <h1>Section above: Faces only</h1>
  <Text />
  <TextOnly />
  <h1>Section above: Text Only</h1>
  <Text />
  <OnomatopoeiaOnly />
  <h1>Section above: Onomatopoeia Only</h1>
  <Text />
</main>
