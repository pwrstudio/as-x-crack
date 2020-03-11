<script>
  // *** COMPONENTS
  import { fade } from "svelte/transition";
  import _ from "lodash";

  import { combos, imageIndices, onomatos } from "./global.js";

  const randomInRange = (min, max) => {
    min = Math.ceil(min);
    max = Math.floor(max);
    return Math.floor(Math.random() * (max - min + 1)) + min;
  };

  let wordOne = false;
  let wordTwo = false;
  let wordThree = false;

  let faceOne = false;
  let faceTwo = false;
  let faceThree = false;

  let onoOne = false;
  let onoTwo = false;
  let onoThree = false;

  let symbolOne = false;
  let symbolTwo = false;
  let symbolThree = false;

  const prob = [
    "word",
    "word",
    "word",
    "word",
    "word",
    "word",
    "word",
    "word",
    "word",
    "word",
    "word",
    "image",
    "image",
    "image",
    "image",
    "image",
    "ono",
    "ono",
    "ono",
    "symbol",
    "symbol"
  ];

  const updateScreen = () => {
    wordOne = false;
    wordTwo = false;
    wordThree = false;

    faceOne = false;
    faceTwo = false;
    faceThree = false;

    onoOne = false;
    onoTwo = false;
    onoThree = false;

    symbolOne = false;
    symbolTwo = false;
    symbolThree = false;

    setTimeout(() => {
      let imageSet = _.sampleSize(imageIndices, 3);
      let currentFrame = _.sample(combos);

      // 11111

      let randomOne = _.sample(prob);
      if (randomOne == "ono") {
        onoOne = _.sample(onomatos);
      } else if (randomOne == "symbol") {
        symbolOne = "symbols/" + randomInRange(2, 2) + "-symbol.png";
      } else {
        wordOne = currentFrame[0];
      }

      // // 22222
      let randomTwo = _.sample(prob);
      if (randomTwo == "ono") {
        onoTwo = _.sample(onomatos);
      } else if (randomTwo == "symbol") {
        symbolTwo = "symbols/" + randomInRange(2, 2) + "-symbol.png";
      } else if (randomTwo == "image") {
        faceTwo = "faces/" + imageSet[1] + "-face.jpg";
      } else {
        wordTwo = currentFrame[1];
      }

      // // 33333
      let randomThree = _.sample(prob);
      if (randomThree == "ono") {
        onoThree = _.sample(onomatos);
      } else if (randomThree == "symbol") {
        symbolThree = "symbols/" + randomInRange(2, 2) + "-symbol.png";
      } else if (randomThree == "image" && !faceTwo) {
        faceThree = "faces/" + imageSet[2] + "-face.jpg";
      } else {
        wordThree = currentFrame[2];
      }
    }, 100);
  };

  setInterval(updateScreen, 3000);

  updateScreen();
</script>

<style>
  .poetry {
    width: 600px;
    height: 600px;
    background: black;
    width: 100vw;
    height: 100vh;
    background: orangered;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .word {
    display: inline-block;
    color: black;
    object-fit: cover;
    text-align: center;
    font-family: Arial;
    font-weight: bold;
    font-size: 9vw;
    user-select: none;
    letter-spacing: -0.3vw;
  }

  .spaced {
    padding-right: 2vw;
  }

  .face {
    width: 32vw;
    height: 32vw;
  }

  .slapstick {
    letter-spacing: -0.2vw;
    z-index: 100;
    font-size: 12vw;
    font-family: "comic_marker_deluxeregular" !important;
    /* color: #00ff00; */
    transform: rotateZ(20deg) translateY(-20px);
  }

  .symbol {
    width: 30vw;
  }
</style>

<div class="poetry">

  <!-- 11111 -->
  {#if wordOne}
    <span class="word spaced" in:fade={{ delay: 0 }}>{wordOne}</span>
  {/if}
  {#if onoOne}
    <span class="word slapstick spaced" in:fade={{ delay: 0 }}>{onoOne}</span>
  {/if}
  {#if symbolOne}
    <img class="symbol spaced" src={symbolOne} in:fade={{ delay: 0 }} />
  {/if}

  <!-- 22222 -->
  {#if wordTwo}
    <span class="word spaced" in:fade={{ delay: 200 }}>{wordTwo}</span>
  {/if}
  {#if faceTwo}
    <img class="face spaced" src={faceTwo} in:fade={{ delay: 200 }} />
  {/if}
  {#if onoTwo}
    <span class="word slapstick spaced" in:fade={{ delay: 200 }}>{onoTwo}</span>
  {/if}
  {#if symbolTwo}
    <img class="symbol spaced" src={symbolTwo} in:fade={{ delay: 200 }} />
  {/if}

  <!-- 33333 -->
  {#if wordThree}
    <span class="word" in:fade={{ delay: 400 }}>{wordThree}</span>
  {/if}
  {#if faceThree}
    <img class="face" src={faceThree} in:fade={{ delay: 400 }} />
  {/if}
  {#if onoThree}
    <span class="word slapstick" in:fade={{ delay: 400 }}>{onoThree}</span>
  {/if}
  {#if symbolThree}
    <img class="symbol spaced" src={symbolThree} in:fade={{ delay: 400 }} />
  {/if}

</div>
