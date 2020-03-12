<script>
  // *** COMPONENTS
  import { fade } from "svelte/transition";
  import _ from "lodash";

  import { combos, imageIndices } from "./global.js";

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
    "image"
  ];

  const updateScreen = () => {
    wordOne = false;
    wordTwo = false;
    wordThree = false;

    faceOne = false;
    faceTwo = false;
    faceThree = false;

    setTimeout(() => {
      let currentFrame = _.sample(combos);
      let imageSet = _.sampleSize(imageIndices, 3);

      // 11111
      wordOne = currentFrame[0];

      // // 22222
      let randomTwo = _.sample(prob);
      if (randomTwo == "image") {
        faceTwo = "faces/" + imageSet[1] + "-face.jpg";
      } else {
        wordTwo = currentFrame[1];
      }

      // // 33333
      let randomThree = _.sample(prob);
      if (randomThree == "image" && !faceTwo) {
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
    background: rgb(255, 68, 0);
    background-color: #00ff00;
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
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
    z-index: 10;
  }

  .spaced {
    padding-right: 2vw;
  }

  .face {
    width: 32vw;
    height: 32vw;
    z-index: 10;
  }

  video {
    position: absolute;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    object-fit: cover;
    /* opacity: 0.6; */
    mix-blend-mode: difference;
    /* filter: grayscale(1); */
  }

  .bg {
    position: absolute;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    object-fit: cover;
    opacity: 0.4;
    mix-blend-mode: multiply;
    filter: grayscale(1);
  }

  @media only screen and (max-width: 700px) {
    .poetry {
      flex-direction: column;
    }

    .word {
      display: block;
      font-size: 28vw;
      letter-spacing: -0.5vw;
    }

    .spaced {
      padding-right: 0;
    }

    .face {
      width: 60vw;
      height: 60vw;
    }
  }
</style>

<div class="poetry">

  <video src="/media/fire.mp4" autoplay loop muted />
  <!-- <img src="/media/hill.png" class="bg" /> -->

  <!-- 11111 -->
  {#if wordOne}
    <span class="word spaced" in:fade={{ delay: 0 }}>{wordOne}</span>
  {/if}

  <!-- 22222 -->
  {#if wordTwo}
    <span class="word spaced" in:fade={{ delay: 200 }}>{wordTwo}</span>
  {/if}
  {#if faceTwo}
    <img class="face spaced" src={faceTwo} in:fade={{ delay: 200 }} />
  {/if}

  <!-- 33333 -->
  {#if wordThree}
    <span class="word" in:fade={{ delay: 400 }}>{wordThree}</span>
  {/if}
  {#if faceThree}
    <img class="face" src={faceThree} in:fade={{ delay: 400 }} />
  {/if}

</div>
