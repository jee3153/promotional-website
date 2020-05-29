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

  const openHome = async () => {
    menuOpen.update(value => false);
    projectPage.update(value => false);
    skillPage.update(value => false);
    rightFacestatus.update(value => "");
    main.update(value => true);
    await tick();
    soundPlay("oilSquart");
  };
</script>

<div
  class="home-btn"
  on:click="{() => openHome()}"
  in:fly="{{ delay: 700, opacity: 0, x: 2000, duration: 500, easing: sineInOut }}"
  out:fade
>
  <span class="direct-btn text-style">Who am I?</span>
  <img class=" drill" src="images/tool7.png" alt="drill" />
</div>

<style>
  .drill {
    width: 42px;
    animation: drilling 3s ease-in-out infinite;
  }
  .home-btn {
    margin-bottom: 1.5rem;
  }

  @media (min-width: 640px) {
    .direct-btn {
      width: 6rem;
    }
  }
  @media (min-width: 1000px) {
  }
</style>
