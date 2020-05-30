<script>
  import { main, menuOpen, skillPage, projectPage } from "../stores.js";
  import { slide, scale, fade, fly } from "svelte/transition";
  import { quadInOut, bounceInOut } from "svelte/easing";

  import DirectingLinks from "./nav/DirectingLinks.svelte";
  import Spanner from "./nav/Spanner.svelte";
  import Drill from "./nav/Drill.svelte";

  export let soundPlay;

  let selected = "shopping cart";
  const images = [
    {
      name: "shopping cart",
      path: "shopping-cart",
      href: "https://ji90-shopping-cart.netlify.app/"
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
  <section>

    <div class="nav-container">
      <DirectingLinks>
        <Drill {soundPlay} />
        <Spanner {soundPlay} />
      </DirectingLinks>
    </div>

    <div class="heading">
      <img class="tools" src="images/smallertoolssm.png" alt="" />
      <h1>
        I build things to solve
        <span class="highlighter">problems</span>
        and to reflect my
        <span class="highlighter">interest</span>
        at the time.
      </h1>
    </div>

    <div
      class="trigger-container"
      transition:fly="{{ opacity: 0, duration: 100, easing: bounceInOut }}"
    >
      {#each images as { name, path }, i}
        <div
          class="trigger"
          style="background-image:url(images/thumnail-{path}.png);"
          on:click="{() => (selected = name)}"
        ></div>
      {/each}
    </div>

    <div class="container">
      {#each images as { name, path, href }, i}
        {#if selected === name}
          <h1 class="text-style project-title {path}">{name}</h1>
          <div class="sub-container">
            <a class="link" {href} target="_blank">
              <div
                class="prj-{i + 1} project"
                style="background-image:url(images/{path}.png);"
              ></div>

            </a>
            {#if selected === 'shopping cart'}
              <p class="description">
                Shopping cart app that works perfectly in native and web using
                web environment development technology. Implementation of
                calculators of tips of your choice and swiping gestures. Cart
                item will remain even after browser is refreshed or closed cart
                item Techonology used:
                <span class="highlighter">React</span>
                ,
                <span class="highlighter">Tailwind</span>
              </p>
            {:else if selected === 'tamago game'}
              <p class="description">
                Pet raising game that is inspired by 90's tamagotchi. Technology
                used:
                <span class="highlighter">JavaScript</span>
                , Phaser.js, Animations
              </p>
            {:else if selected === 'what to weather'}
              <p class="description">
                Weather SPA (Single Page Application) that gives you an idea of
                daily outfit based on temperature of the day used technology:
                <span class="highlighter">react</span>
                ,
                <span class="highlighter">scss</span>
              </p>
            {/if}
          </div>
        {/if}
      {/each}
    </div>

  </section>
{/if}

<style>
  section {
    overflow-x: hidden;
    width: 100vw;
    height: 100vh;
    position: relative;
  }
  .heading {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 1rem 2rem;
    text-align: center;
  }
  .tools {
    width: 17%;
  }
  .container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 100%;
  }
  .nav-container {
    position: relative;
    padding: 1rem 2rem;
    width: 94%;
    height: 113px;
    margin-bottom: 1rem;
  }
  .sub-container {
    width: 100%;
    height: 44%;
  }
  .project-title {
    padding: 0 1rem;
  }
  .project {
    background-repeat: no-repeat;
    background-position: center;
    background-size: 80%;
    background-color: black;
    opacity: 1;
    transition: background-size 0.4s linear;
    filter: grayscale(1);
    width: 100%;
    height: 100%;
  }
  .project:active {
    filter: grayscale(0);
  }
  .description {
    text-align: center;
    font-size: 1.4rem;
    padding: 1.4rem;
  }
  .trigger-container {
    padding: 1rem 2rem;
    display: flex;
    justify-content: center;
  }
  .trigger {
    margin: 0 1rem;
    width: 30px;
    height: 40px;
    background-color: black;
    background-size: 100%;
    background-position: center;
    border-radius: 10%;
    background-repeat: no-repeat;
    transition: background-size 0.3s linear;
  }

  @media (min-width: 640px) {
    .container {
      justify-content: flex-start;
    }
    .sub-container {
      width: 100%;
      height: 100%;
      margin-top: 1rem;
    }
    .trigger {
      width: 70px;
      height: 92px;
    }
    .trigger:hover {
      background-size: 120%;
    }
    .nav-container {
      margin-bottom: 5rem;
    }
  }
  @media (min-width: 1000px) {
    .nav-container {
      padding: 2rem;
    }
    .container {
      padding: 1rem 2rem;
      width: 94%;
      margin-bottom: 4rem;
      height: 70%;
    }
    .sub-container {
      display: flex;
      align-items: center;
      justify-content: space-evenly;
    }
    .description {
      text-align: left;
      max-width: 314px;
    }
    .project {
      width: 50vw;
      height: 42rem;
      max-width: 433px;
    }
    .description {
      padding: 0 2rem;
    }
    .prj-2 {
      width: 60vw;
      height: 25rem;
      max-width: 693px;
    }
  }
</style>
