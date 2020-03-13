<script>
  // *** COMPONENTS
  import { fade } from "svelte/transition";
  import _ from "lodash";

  import { onomatos } from "./global.js";

  const randomInRange = (min, max) => {
    min = Math.ceil(min);
    max = Math.floor(max);
    return Math.floor(Math.random() * (max - min + 1)) + min;
  };

  let onoOne = false;
  let onoTwo = false;
  let onoThree = false;

  let symbolOne = false;
  let symbolTwo = false;
  let symbolThree = false;

  const prob = ["ono", "ono", "ono", "ono", "ono", "symbol"];

  const updateScreen = () => {
    onoOne = false;
    onoTwo = false;
    onoThree = false;

    symbolOne = false;
    symbolTwo = false;
    symbolThree = false;

    setTimeout(() => {
      // 11111
      onoOne = _.sample(onomatos);

      // // 22222
      let randomTwo = _.sample(prob);
      if (randomTwo == "ono") {
        onoTwo = _.sample(onomatos);
      } else if (randomTwo == "symbol") {
        symbolTwo = "symbols/" + randomInRange(2, 2) + "-symbol.png";
      }

      // // 33333
      let randomThree = _.sample(prob);
      if (randomThree == "ono") {
        onoThree = _.sample(onomatos);
      } else if (randomThree == "symbol") {
        symbolThree = "symbols/" + randomInRange(2, 2) + "-symbol.png";
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
    background: rgb(255, 0, 200);

    /* background: #00ff00;
    background: red; */
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .word {
    display: inline-block;
    object-fit: cover;
    text-align: center;
    font-family: Arial;
    font-weight: bold;
    font-size: 9vw;
    user-select: none;
    letter-spacing: -0.3vw;
    color: black;
  }

  .spaced {
    padding-right: 2vw;
  }

  .slapstick {
    letter-spacing: -0.2vw;
    z-index: 100;
    font-size: 12vw;
    font-family: "comic_marker_deluxeregular" !important;
    transform: rotateZ(20deg) translateY(-20px);
  }

  .symbol {
    width: 30vw;
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

    .slapstick {
      font-size: 26vw;
    }

    .symbol {
      width: 50vw;
    }
  }
</style>

<div class="poetry">

  <!-- 11111 -->
  {#if onoOne}
    <span class="word slapstick spaced" in:fade={{ delay: 0 }}>{onoOne}</span>
  {/if}
  {#if symbolOne}
    <img class="symbol spaced" src={symbolOne} in:fade={{ delay: 0 }} />
  {/if}

  <!-- 22222 -->
  {#if onoTwo}
    <span class="word slapstick spaced" in:fade={{ delay: 200 }}>{onoTwo}</span>
  {/if}
  {#if symbolTwo}
    <img class="symbol spaced" src={symbolTwo} in:fade={{ delay: 200 }} />
  {/if}

  <!-- 33333 -->
  {#if onoThree}
    <span class="word slapstick" in:fade={{ delay: 400 }}>{onoThree}</span>
  {/if}
  {#if symbolThree}
    <img class="symbol spaced" src={symbolThree} in:fade={{ delay: 400 }} />
  {/if}

</div>
