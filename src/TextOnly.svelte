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
  .poetry {
    width: 600px;
    height: 600px;
    background: black;
    width: 100vw;
    height: 100vh;
    background: rgb(255, 68, 0);
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
    font-size: 10vw;
    user-select: none;
    letter-spacing: -0.5vw;
  }

  .spaced {
    padding-right: 2vw;
  }

  @media only screen and (max-width: 700px) {
    .poetry {
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

<div class="poetry">

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
