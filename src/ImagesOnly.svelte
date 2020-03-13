<script>
  // *** COMPONENTS
  import { fade } from "svelte/transition";
  import _ from "lodash";

  import { imageIndices } from "./global.js";

  const randomInRange = (min, max) => {
    min = Math.ceil(min);
    max = Math.floor(max);
    return Math.floor(Math.random() * (max - min + 1)) + min;
  };

  let faceOne = false;
  let faceTwo = false;
  let faceThree = false;

  const updateScreen = () => {
    faceOne = false;
    faceTwo = false;
    faceThree = false;

    setTimeout(() => {
      let imageSet = _.sampleSize(imageIndices, 3);
      // 11111
      faceOne = "faces/" + imageSet[0] + "-face.jpg";

      // // 22222
      faceTwo = "faces/" + imageSet[1] + "-face.jpg";

      // // 33333
      faceThree = "faces/" + imageSet[2] + "-face.jpg";
    }, 100);
  };

  setInterval(updateScreen, 3000);

  updateScreen();
</script>

<style>
  .images-only {
    width: 600px;
    height: 600px;
    background: black;
    width: 100vw;
    height: 100vh;
    background: rgb(255, 68, 0);
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
  }

  .spaced {
    padding-right: 2vw;
  }

  .face {
    width: 31vw;
    height: 31vw;
    z-index: 1000;
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
    .images-only {
      height: 190vw;
      flex-direction: column;
    }

    .spaced {
      padding-right: 0;
      margin-bottom: 2vw;
    }

    .face {
      width: 60vw;
      height: 60vw;
    }
  }
</style>

<div class="images-only">

  <img src="/media/wall.png" class="bg" />

  <!-- 11111 -->
  {#if faceOne}
    <img class="face spaced" src={faceOne} in:fade={{ delay: 0 }} />
  {/if}

  <!-- 22222 -->
  {#if faceTwo}
    <img class="face spaced" src={faceTwo} in:fade={{ delay: 200 }} />
  {/if}

  <!-- 33333 -->
  {#if faceThree}
    <img class="face" src={faceThree} in:fade={{ delay: 400 }} />
  {/if}

</div>
