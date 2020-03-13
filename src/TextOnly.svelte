<script>
  // *** COMPONENTS
  import { fade, slide, fly } from "svelte/transition";
  import _ from "lodash";

  import { combos } from "./global.js";

  let wordOne = false;
  let wordTwo = false;
  let wordThree = false;

  const updateScreen = () => {
    wordOne = false;
    wordTwo = false;
    wordThree = false;

    setTimeout(() => {
      let currentFrame = _.sample(combos);

      // 11111
      wordOne = currentFrame[0];

      // 22222
      wordTwo = currentFrame[1];

      // 33333
      wordThree = currentFrame[2];
    }, 100);
  };

  setInterval(updateScreen, 3000);

  updateScreen();
</script>

<style>
  .text-only {
    width: 600px;
    height: 600px;
    background: black;
    width: 100vw;
    height: 100vh;
    background: rgb(255, 68, 0);
    background: #00ff00;
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
    font-size: 10vw;
    user-select: none;
    letter-spacing: -0.5vw;
    z-index: 100;
  }

  .spaced {
    padding-right: 2vw;
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
    opacity: 0.2;
  }

  @media only screen and (max-width: 700px) {
    .text-only {
      flex-direction: column;
    }

    .word {
      display: block;
      font-size: 24vw;
      letter-spacing: -0.3vw;
    }

    .spaced {
      padding-right: 0;
    }

    .face {
      width: 50vw;
      height: 50vw;
    }
  }
</style>

<div class="text-only">

  <img src="/media/window.png" class="bg" />

  <!-- 11111 -->
  {#if wordOne}
    <span class="word spaced" in:fade={{ delay: 0 }}>{wordOne}</span>
  {/if}

  <!-- 22222 -->
  {#if wordTwo}
    <span class="word spaced" in:fade={{ delay: 200 }}>{wordTwo}</span>
  {/if}

  <!-- 33333 -->
  {#if wordThree}
    <span class="word" in:fade={{ delay: 400 }}>{wordThree}</span>
  {/if}

</div>
