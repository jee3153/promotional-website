<script>
  import { onMount, onDestroy } from "svelte";

  import Brain from "./components/Brain.svelte";
  import RightFace from "./components/RightFace.svelte";
  import LeftFace from "./components/LeftFace.svelte";
  import TrainingSkills from "./components/TrainingSkills.svelte";
  import ProjectBuilt from "./components/ProjectBuilt.svelte";
  import DirectingLinks from "./components/nav/DirectingLinks.svelte";

  import { main } from "./stores.js";

  let soundPlay = soundId => {
    const audio = document.getElementById(soundId);
    audio.play();
  };
  let mounted = false;
  let sounds = ["metalSound", "hammering", "spanning", "oilSquart"];
  // const unsubscribe = main.subscribe(value => {
  //   mainPage = main;
  // });

  onMount(() => {
    mounted = true;
    console.log("mounted");
  });
  onDestroy(() => {
    console.log("destroyed");
  });
</script>

<main>
  <Brain {soundPlay} />
  <LeftFace />
  <TrainingSkills {soundPlay} />
  <RightFace />
  <ProjectBuilt {soundPlay} />
  {#each sounds as sound}
    <audio id="{sound}" src="sound/{sound}.mp3"></audio>
  {/each}
</main>

<style>
  @import url("https://use.typekit.net/uuh1zkm.css");
  @keyframes -global-drilling {
    30% {
      transform: translate(15px, 2px);
    }
    50% {
      transform: translate(30px, 4px);
    }
    100% {
      transform: translate(0);
    }
  }
  @keyframes -global-spanning {
    53% {
      transform: rotate(20deg);
    }
    60% {
      transform: rotate(40deg);
    }
    80% {
      transform: rotate(60deg);
    }
    100% {
      transform: rotate(0deg);
    }
  }
  @keyframes -global-hammering {
    50% {
      transform: rotate(8deg);
    }
    80% {
      transform: rotate(30deg);
    }
    100% {
      transform: rotate(10deg);
    }
  }
  @keyframes -global-blink {
    100% {
      color: #727171;
    }
  }
  @keyframes -global-partsLotation1 {
    100% {
      transform: rotate(360deg);
    }
  }
  @keyframes -global-partsLotation2 {
    100% {
      transform: rotate(-360deg);
    }
  }
  :global(body, html) {
    margin: 0;
    padding: 0;
    overflow-x: hidden;
    color: #3a3ca1;
  }

  :global(section, div, button) {
    font-family: garamond-fb-display, serif;
    font-weight: 400;
    font-size: 25px;
  }

  :global(h1) {
    font-family: adobe-caslon-pro, serif;
    font-weight: 700;
  }

  :global(.text-style) {
    background: #3a3ca1;
    color: #fff;
  }
  :global(.direct-btn) {
    font-size: 19px;
  }

  main {
    font-family: adobe-caslon-pro;
    font-weight: 700;
    font-style: italic;
    font-size: 3rem;
    width: 100vw;
    height: 100vh;
    background-color: #fbe0d1;
    display: grid;
    grid-template-columns: repeat(4, minmax(0, 1fr));
    grid-template-rows: 12.5% 12.5% 18% 1fr 1fr 15%;
    grid-template-areas:
      "header header header header"
      "header header header header"
      "additional additional main main"
      "additional additional main main"
      "additional additional main main"
      "footer footer footer footer";
  }

  @media (min-width: 640px) {
    :global(.home-btn:hover, .skills-btn:hover, .project-btn:hover) {
      transform: scale(1.2);
    }
    :global(.direct-btn) {
      font-size: 24px;
    }
    :global(.home-btn, .project-btn, .skills-btn) {
      display: grid;
      position: absolute;
      cursor: pointer;
      width: 0;
      transition: transform ease 0.5s;
    }
    main {
      max-width: none;
    }
  }
</style>
