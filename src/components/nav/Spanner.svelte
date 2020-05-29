<script>
  import { tick } from "svelte";
  import {
    main,
    menuOpen,
    skillPage,
    projectPage,
    rightFacestatus
  } from "../../stores.js";
  import { fly, fade } from "svelte/transition";
  import { sineInOut } from "svelte/easing";
  export let soundPlay;

  const openSkils = async () => {
    main.update(value => false);
    menuOpen.update(value => false);
    projectPage.update(value => false);
    rightFacestatus.update(value => "");
    skillPage.update(value => true);
    await tick();
    soundPlay("spanning");
  };
</script>

<div
  class="skills-btn"
  on:click="{() => openSkils()}"
  transition:fly="{{ opacity: 0, x: 100, y: 60, duration: 500, easing: sineInOut }}"
>
  <span class="direct-btn text-style">Training Skills</span>
  <img class="spanner" src="images/spanner.png" alt="spanner" />
</div>

<style>
  .spanner {
    width: 100px;
    transform-origin: 5% 5%;
    animation: spanning 2s linear infinite;
  }
  @media (min-width: 640px) {
    .skills-btn {
      left: 93%;
    }
    .direct-btn {
      width: 8rem;
    }
  }
  @media (min-width: 1000px) {
  }
</style>
