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
  let screenSize = window.innerWidth;
  const openSkils = async () => {
    main.update(value => false);
    menuOpen.update(value => false);
    projectPage.update(value => false);
    rightFacestatus.update(value => "");
    skillPage.update(value => true);
    await tick();
    soundPlay("spanning");
  };
  const locationChanger = () => {
    if (screenSize >= 640) {
      if ($projectPage) return "top:74%;";
      else if ($main) return "right:16%;";
    }
  };
</script>

<div
  class="skills-btn"
  on:click="{() => openSkils()}"
  transition:fly="{{ opacity: 0, x: 100, y: 60, duration: 500, easing: sineInOut }}"
  style="{locationChanger()}"
>
  <span class="direct-btn text-style">Training Skills</span>
  <img class="spanner" src="images/spanner.png" alt="spanner" />
</div>

<style>
  .spanner {
    width: 52px;
    transform-origin: 5% 5%;
    animation: spanning 2s linear infinite;
  }
  @media (min-width: 640px) {
    .direct-btn {
      width: 8rem;
    }
  }
  @media (min-width: 1000px) {
  }
</style>
