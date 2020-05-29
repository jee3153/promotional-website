<script>
  import { main, rightFacestatus, menuOpen } from "../stores.js";
  import { slide, scale } from "svelte/transition";
  import { quadInOut } from "svelte/easing";
  import DirectingLinks from "./nav/DirectingLinks.svelte";
  import Hammer from "./nav/Hammer.svelte";
  import Spanner from "./nav/Spanner.svelte";

  export let soundPlay;

  const clickHandler = e => {
    menuOpen.update(value => !$menuOpen);
    soundPlay("metalSound");
  };
</script>

{#if $main}
  <h1
    transition:scale="{{ delay: 600, opacity: 0, start: 0, duration: 500, easing: quadInOut }}"
  >
    I am a software engineer.
  </h1>
  <div
    class="machine-brain {$main ? 'visible' : 'invisible'}"
    style="background-image:url(/images/partcombined.png); {!$main ? 'width:36vw;' : 'width:46vw;'}"
    transition:scale="{{ delay: 500, opacity: 0, start: 0, duration: 500, easing: quadInOut }}"
  >
    <div class="menu-container">
      <div
        class="menu-btn"
        on:click="{clickHandler}"
        style="{$menuOpen ? 'transform:scale(2);' : 'transform:scale(1);'}"
      >
        {#if !$menuOpen}
          <span class="click-me btn">Click me!'</span>
        {:else}
          <span class="close-me btn">Close me!</span>
        {/if}

        <img class="part-3" src="images/part-3.png" alt="part-3" />
      </div>
      {#if $menuOpen}
        <div class="nav-container">
          <DirectingLinks>
            <span class="hammer-container">
              <Hammer {soundPlay} />
            </span>
            <span class="spanner-container">
              <Spanner {soundPlay} />
            </span>

          </DirectingLinks>
        </div>
      {/if}
    </div>

    <img class="part-1" src="images/part-1.png" alt="part-1" />
    <img class="part-5" src="images/part-5.png" alt="part-5" />

    <!-- <audio id="clickSound" src="sound/metalSound.mp3"></audio> -->
  </div>
{/if}

<style>
  h1 {
    font-size: 3rem;
    grid-area: header;
    position: absolute;
    z-index: 0;
    text-align: center;
    line-height: 1;
  }
  div {
    position: relative;
  }

  .btn {
    color: white;
    background: #3a3ca1;
    position: absolute;
    display: block;
  }
  .click-me {
    animation: blink 0.8s linear infinite;
    top: -22px;
    left: 0;
    font-size: 1.2rem;
  }
  .close-me {
    top: 36px;
    left: 36px;
    font-size: 0.8rem;
  }
  .menu-container {
    top: 27%;
    left: 0;
  }
  .menu-btn {
    left: 64%;
    top: 28%;
    width: 30vw;
    transition: all 0.3s ease-in-out;
    cursor: pointer;
  }
  .menu-btn:hover {
    transform: scale(2);
  }

  .part-3,
  .part-1,
  .part-5 {
    position: absolute;
  }

  .machine-brain {
    z-index: 2;
    top: 12%;
    background-position: center;
    background-size: contain;
    background-repeat: no-repeat;
    max-width: 200px;
    height: 29vh;
    transition: transform 0.4s linear 0.6s;
    grid-area: 2 / 2 / span 2 / span 2;
    justify-self: center;
  }

  .part-3,
  .part-1 {
    z-index: 3;
  }
  .part-3 {
    cursor: pointer;
    top: 70%;
    left: 10%;
    width: 33%;
    max-width: 46px;
    animation: partsLotation1 1s linear infinite;
  }
  .part-1 {
    top: 45%;
    left: 10%;
    width: 15%;
    animation: partsLotation2 5s linear infinite;
  }

  .part-5 {
    top: 44%;
    left: 67%;
    width: 13%;
    z-index: -1;
    animation: partsLotation2 10s linear infinite;
  }
  .nav-container {
    top: -18vh;
    left: -11vh;
  }

  @media (min-width: 640px) {
    h1 {
      font-size: 6rem;
      width: 9rem;
      margin-left: 3rem;
    }
    .machine-brain {
      transform: scale(1.5);
    }
    .part-5 {
      top: 47%;
      left: 68%;
      width: 10%;
      animation: partsLotation2 10s linear infinite;
    }
    .menu-container {
      top: 36%;
    }
    .close-me {
      top: 46px;
    }
    .click-me {
      left: 6%;
    }
    .nav-container {
      top: -12vh;
      left: -4vh;
    }
    .hammer-container {
      position: relative;
      left: 0;
    }
  }
  @media (min-width: 1000px) {
    .part-3 {
      left: 5%;
    }
  }
</style>
