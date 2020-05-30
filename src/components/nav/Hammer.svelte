<script>
  import { tick } from "svelte";
  import { fly, fade } from "svelte/transition";
  import { sineInOut } from "svelte/easing";
  import { main, menuOpen, skillPage, projectPage } from "../../stores.js";

  export let soundPlay;
  let screenSize = window.innerWidth;
  const openProject = async () => {
    main.update(value => false);
    menuOpen.update(value => false);
    skillPage.update(value => false);
    projectPage.update(value => true);
    await tick();
    soundPlay("hammering");
  };

  const locationChanger = () => {
    if (screenSize >= 640) {
      if ($main) return "top:9%;";
      else return "top:44%;";
    }
  };
</script>

<div
  class="project-btn"
  on:click="{() => openProject()}"
  transition:fly="{{ opacity: 0, x: 100, duration: 500, easing: sineInOut }}"
  style="{locationChanger()}"
>
  <span class="direct-btn text-style">What I built</span>
  <img class="hammer" src="images/hammer.png" alt="hammer" />
</div>

<style>
  .hammer {
    width: 65px;
    z-index: 1;
    animation: hammering 1s linear infinite;
  }

  @media (min-width: 640px) {
    .direct-btn {
      width: 100px;
    }
  }
  @media (min-width: 1000px) {
    /* .project-btn {
      left: -10vh;
    } */
  }
</style>
