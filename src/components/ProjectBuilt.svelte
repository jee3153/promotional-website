<script>
  import { main, menuOpen, skillPage, projectPage } from "../stores.js";
  import { slide, scale, fade, fly } from "svelte/transition";
  import { quadInOut, bounceInOut } from "svelte/easing";

  import DirectingLinks from "./nav/DirectingLinks.svelte";
  import Spanner from "./nav/Spanner.svelte";
  import Drill from "./nav/Drill.svelte";

  export let soundPlay;

  let selected;
  const images = [
    {
      name: "shopping cart",
      path: "shopping-cart",
      href: "https://github.com/jee3153/shoppingcart"
    },
    {
      name: "tamago game",
      path: "tamago-game",
      href: "https://ji90tamagogame.netlify.app/"
    },
    {
      name: "what to weather",
      path: "whattoweather",
      href: "https://jee3153.github.io/WhatToWeather-react/"
    }
  ];
</script>

{#if $projectPage}
  <section
    out:fly="{{ delay: 2000, x: -2000, opacity: 0, duration: 800, easing: bounceInOut }}"
  >
    <div
      transition:fly="{{ x: -2000, opacity: 0, duration: 800, easing: bounceInOut }}"
    >
      <h1>I have built...</h1>
      <p class="instruction">More projects are coming!</p>
    </div>

    <img
      class="globe"
      src="images/antique-map.png"
      alt="globe"
      transition:fly="{{ y: -2000, opacity: 0, duration: 1500, easing: quadInOut }}"
    />
    <img
      class="compass-face"
      src="images/compass-face.png"
      alt="compass-face"
      transition:fly="{{ delay: 200, x: -2000, opacity: 0, duration: 500, easing: quadInOut }}"
    />
    <img
      class="skull"
      src="images/skull.png"
      alt="skull"
      transition:scale="{{ opacity: 0, start: 0, duration: 300, easing: quadInOut }}"
    />

    <div
      class="link-container"
      transition:slide="{{ delay: 600, opacity: 0, duration: 300, easing: quadInOut }}"
    >

      {#each images as { name, path }, i}
        <div
          class="prj-{i + 1} link"
          style="background-image:url(images/thumnail-{path}.png);"
          on:click="{() => (selected = name)}"
          out:fade="{{ delay: 1500, duration: 3000, easing: quadInOut }}"
        ></div>
      {/each}

    </div>

    {#each images as { name, path, href }, i}
      {#if selected === name}
        <a
          {href}
          out:scale="{{ opacity: 0, start: 0, duration: 200, easing: quadInOut }}"
        >
          <img
            class="bigger-view"
            src="images/{path}.png"
            alt="project scaled"
          />
          <p class="text-style project-title {path}">{name}</p>
        </a>
      {/if}
    {/each}
    <div
      out:scale="{{ opacity: 0, start: 0, duration: 200, easing: quadInOut }}"
    >
      {#if selected === 'shopping cart'}
        <p class="description">
          Shopping cart app that works perfectly in native and web using web
          environment development technology. Implementation of calculators of
          tips of your choice and swiping gestures. Cart item will remain even
          after browser is refreshed or closed cart item Techonology used:
          React, Tailwind
        </p>
      {:else if selected === 'tamago game'}
        <p class="description">
          Pet raising game that is inspired by 90's tamagotchi. Technology used:
          JavaScript, Phaser.js, Animations
        </p>
      {:else if selected === 'what to weather'}
        <p class="description">
          Weather SPA (Single Page Application) that gives you an idea of daily
          outfit based on temperature of the day used technology: react, scss
        </p>
      {/if}
    </div>

    <div class="nav-container">
      <DirectingLinks>
        <Drill {soundPlay} />
        <Spanner {soundPlay} />
      </DirectingLinks>
    </div>

  </section>
{/if}

<style>
  section {
    width: 100vw;
    height: 100vh;
    position: relative;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
  h1 {
    top: 3%;
    width: 70vw;
  }
  .instruction {
    top: 12%;
  }
  h1,
  .instruction {
    color: white;
    position: absolute;
    transform: translate(-50%, -50%);
    left: 50%;
    text-align: center;

    z-index: 1;
  }

  .globe {
    position: absolute;
    width: 100vw;
    top: -28%;
    animation: partsLotation1 12s linear infinite;
    opacity: 0.5;
  }
  .compass-face {
    position: absolute;
    width: 30vw;
    top: 7%;
    left: 0;
    animation: partsLotation2 12s linear infinite;
  }
  .skull {
    position: absolute;
    width: 90vw;
    top: 18vh;
    left: 5vw;
    max-width: 720px;
  }
  .link-container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    justify-items: center;
    position: relative;
    top: -15vh;
    height: 20vh;
  }
  .link {
    cursor: pointer;
    width: 20vw;
    background-repeat: no-repeat;
    background-position: center;
    background-size: 100%;
    opacity: 1;
    transition: background-size 0.4s linear;
    filter: grayscale(1);
  }
  .prj-2-link {
    height: 100%;
  }
  .project-title {
    position: absolute;
    top: 90%;
    left: 17%;
  }
  .whattoweather {
    top: 85%;
    left: 13%;
  }
  .shopping-cart {
    top: 90%;
  }
  .tamago-game {
    top: 72%;
  }
  .bigger-view {
    position: absolute;
    width: 40vw;
    top: 48vh;
    left: 10vw;
    max-width: 310px;
  }
  .nav-container {
    position: absolute;
    width: 40%;
    bottom: 5%;
    right: 0;
    z-index: 3;
  }
  .description {
    position: absolute;
    width: 40vw;
    right: 4vw;
    top: 52vh;
    border: #3a3ca1 solid 1.6px;
    border-radius: 10px;
    padding: 1rem;
    background-color: #f7ddcd;
    opacity: 0.8;
    visibility: hidden;
  }
  @media (min-width: 640px) {
    .link:hover {
      background-size: 120%;
      opacity: 1;
      filter: grayscale(0);
    }
    .nav-container {
      width: 123px;
      top: 84%;
      right: 18%;
    }
    .bigger-view {
      width: 34vw;
      top: 48vh;
    }
    .project-title {
      top: 47%;
      left: 65%;
    }
    .description {
      visibility: visible;
    }
  }
  @media (min-width: 1000px) {
    .skull {
      left: 25%;
    }
    .nav-container {
      width: 123px;
      top: 84%;
      right: 13%;
    }
  }
</style>
