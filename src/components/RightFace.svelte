<script>
  import { main, projectPage } from "../stores.js";
  import { scale, fly } from "svelte/transition";
  import { quadInOut } from "svelte/easing";

  import DirectingLinks from "./nav/DirectingLinks.svelte";
</script>

<section>
  {#if !$projectPage}
    <img
      class="right-face"
      src="images/halfFace2.png"
      alt="right face"
      transition:scale="{{ opacity: 0, start: 0, duration: 500, easint: quadInOut }}"
    />
    <img
      class="constructor "
      src="images/constructor.png"
      alt="constructors"
      transition:scale="{{ delay: 500, opacity: 0, start: 0, duration: 500, easint: quadInOut }}"
    />

    {#if $main}
      <h1
        transition:scale="{{ delay: 600, opacity: 0, start: 0, duration: 500, easint: quadInOut }}"
      >
        I am a
      </h1>
      <div
        class="keywords"
        transition:fly="{{ delay: 800, opacity: 0, duration: 300, easint: quadInOut }}"
      >
        <span class="fixer">Fixer</span>
        <span class="builder">Builder</span>
        <span class="learner">Learner</span>
      </div>
    {/if}
  {/if}

</section>

<style>
  @keyframes digging {
    50% {
      transform: rotate(25deg);
    }
    80% {
      transform: rotate(20deg);
    }
    100% {
      transform: rotate(0deg);
    }
  }

  section {
    position: relative;
    grid-area: main;
    width: 50vw;
  }

  span {
    /* position: absolute; */
    display: inline-block;
    z-index: 2;
    left: 25vw;
    color: white;
    background: #3a3ca1;
    margin-bottom: 0.5rem;
  }

  h1 {
    display: inline;
    position: absolute;
    left: -53%;
    top: 71%;
  }
  .keywords {
    position: relative;
    height: 21vh;
    width: 20vw;
    left: 52%;
    top: -33%;
    max-width: 130px;
  }
  .fixer {
    top: 50vh;
    transition: transform 0.1s ease-in-out 1s;
  }
  .builder {
    top: 40vh;
    transition: transform 0.1s ease-in-out 1.1s;
  }
  .learner {
    top: 45vh;
    transition: transform 0.1s ease-in-out 1.2s;
  }

  .right-face {
    width: 34vw;
    max-width: 233px;
    transition: 0.1 ease-in-out 1.3s;
  }

  .constructor {
    position: absolute;
    height: 8rem;
    top: 35%;
    left: 24%;
    max-height: 155px;
    transition: 0.1 ease-in-out 1.5s;
    animation: digging 1.5s ease-in-out infinite;
  }

  @media (min-width: 640px) {
    .constructor {
      height: 15rem;
    }
    .keywords {
      font-size: 3rem;
    }
    h1 {
      top: 70%;
      font-size: 4rem;
    }
  }
</style>
