<script>
  import Brain from "./Brain.svelte";
  import HireForm from "./HireForm.svelte";
  import Drill from "./nav/Drill.svelte";
  import Hammer from "./nav/Hammer.svelte";
  import DirectingLinks from "./nav/DirectingLinks.svelte";
  import { main, hire, skillPage, projectPage, menuOpen } from "../stores.js";
  import { fly, slide, fade } from "svelte/transition";
  import { bounceIn, bounceInOut, sineInOut } from "svelte/easing";
  import anime from "animejs/lib/anime.es.js";

  export let soundPlay;
  const clickHandler = e => {
    menuOpen.update(value => !$menuOpen);
    soundPlay("metalSound");
  };
  let showMySkills = false;
  let screenSize = window.innerWidth;

  let logos = [
    { path: "jslogo", name: "javascript" },
    { path: "react", name: "react" },
    { path: "python", name: "python" },
    { path: "django", name: "django" },
    { path: "postgresql", name: "postgresql" },
    { path: "html", name: "html" },
    { path: "css", name: "css" },
    { path: "svelte", name: "svelte" }
  ];
  let skills = [
    "JavaScript",
    "Python",
    "Django",
    "React",
    "Svelte",
    "SQL",
    "HTML5",
    "CSS3"
  ];

  const randomFloating = () => {
    anime({
      targets: ".logo",
      translateX: () => {
        return anime.random(0, 220);
      },
      translateY: () => {
        return anime.random(0, 93);
      },
      rotate: () => {
        return anime.random(0, 360);
      },
      scale: () => {
        return anime.random(1, 2);
      },
      easing: "linear",
      duration: 2500,
      complete: randomFloating
    });
  };
  const animationStart = () => {
    console.log("animation start trigger");
    randomFloating();
  };

  const skillset = () => {
    showMySkills = true;
  };
</script>

{#if !$main && !$projectPage}
  <section
    class="training-skills"
    transition:fade="{{ delay: 300, opacity: 0, duration: 100, easing: sineInOut }}"
  >
    <div
      class="logos"
      in:fly="{{ delay: 1200, x: -1000, opacity: 0, duration: 400, easing: sineInOut }}"
      out:fade
      on:introend="{animationStart}"
    >
      {#each logos as { path, name }, i}
        <img
          src="images/{path}.png"
          alt="{name}"
          class="logo {name}
          "
          style="{'position:absolute;max-width:56px; width: 7vw;'}"
        />
      {/each}
    </div>
    {#if !showMySkills}
      <h1
        class="text-style"
        style="{'width:70vw;left:50%;'}"
        on:click="{skillset}"
        in:fly="{{ delay: 1000, x: -1000, duration: 400, easing: bounceIn }}"
        out:fade
      >
        What skills under my belt?
      </h1>
    {/if}

    {#if showMySkills}
      <h1
        class="text-style"
        style="{'left:27%;'}"
        in:fly="{{ delay: 700, x: -1000, duration: 400, easing: bounceIn }}"
        out:fade
      >
        Wanna hire me?
      </h1>
    {/if}

    {#if showMySkills}
      <HireForm />
      <div
        class="skillset"
        transition:slide="{{ x: -1000, opacity: 0, easing: bounceInOut }}"
      >
        {#each skills as skill}
          <span class="skill text-style {skill}">{skill}</span>
        {/each}
      </div>
    {/if}

    <img
      class="anatomic-face "
      src="images/anatomical-drawing.png"
      alt="anatomical-drawing"
      transition:slide="{{ delay: 600, x: -1000, duration: 200, easing: bounceInOut }}"
    />
    <div
      class="compass-container"
      transition:fly="{{ delay: 700, y: -1000, opacity: 0, duration: 2000, easing: bounceInOut }}"
    >
      <img
        class="compass {$projectPage ? '' : 'rotating-animation'}"
        src="images/compass.png"
        alt="compass"
      />
    </div>

    <div class="nav-container">
      <DirectingLinks>
        <Drill {soundPlay} />
        <Hammer {soundPlay} />
      </DirectingLinks>
    </div>

  </section>
{/if}

<style type="text/scss">
  @keyframes rotating {
    50% {
      transform: rotate(180deg);
    }
    100% {
      transform: rotate(360deg);
    }
  }
  @keyframes floating {
    30% {
      transform: translateY(3px, 3px);
    }
  }

  section {
    display: flex;
    justify-content: flex-end;
    width: 50vw;
    grid-area: additional;
  }

  h1 {
    display: inline-block;
    position: absolute;
    font-size: 1.5rem;
    top: 3%;
    cursor: pointer;
    z-index: 6;
    left: 15vw;
    transform: translate(-50%, -50%);
    max-width: 420px;
    /* transition: all 0.2s ease-in-out 1.8s; */
  }
  h1:hover,
  span:hover {
    background: #4648bf;
  }
  div {
    position: absolute;
  }
  .anatomic-face {
    height: 67vh;
    /*margin-top: 67vh;*/
    /*position: absolute;
    top: 14vh;
    left: 8vw;
    transition: all 0.2s ease-in-out 1.6s;
    z-index: 0;*/
  }
  .compass {
    transform-origin: 100% 70.85%;
    width: 39vw;
  }

  .rotating-animation {
    animation: rotating 8s linear infinite;
  }
  .compass-container {
    position: absolute;
    width: 0;
    height: 0;
    top: 12vh;
    left: 27vw;
    z-index: 7;
    /* transition: all 0.2s ease-in-out 2s;*/
  }

  .logos {
    position: absolute;
    width: 50vw;
    height: 18vh;
    top: 26vh;
    left: 19%;
    z-index: 7;
    max-width: 400px;
  }

  .skillset {
    z-index: 7;
    width: 30vw;
    left: 5%;
    top: 55%;
    /*transition: opacity 0.5s linear;*/
  }
  .skill {
    display: inline-block;
    margin: 0.2rem;
  }
  .skill:hover {
    background: #3a3ca1;
  }
  .nav-container {
    position: absolute;
    width: 41%;
    bottom: 20%;
    right: 0;
    z-index: 3;
  }
  @media (min-width: 640px) {
    h1 {
      font-size: 2.5rem;
    }
    .nav-container {
      width: 123px;
      top: 84%;
      right: 13%;
    }
  }
  @media (min-width: 1000px) {
    .logos {
      left: 31%;
    }
  }
</style>
