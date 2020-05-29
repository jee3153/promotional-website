<script>
  import { main, rightFacestatus } from "../stores.js";
  import { fly } from "svelte/transition";
  import { bounceInOut, backInOut } from "svelte/easing";
  const leavingEnded = () => {
    rightFacestatus.update(value => "outro ended");
  };
</script>

<section>
  {#if $main}
    <img
      class="left-face {$main ? 'visible' : 'invisible'}"
      src="images/halfFace1.png"
      alt="left face"
      transition:fly="{{ delay: 300, x: -1000, duration: 300, easing: backInOut }}"
    />
    <h1
      class="{$main ? 'visible' : 'invisible'}"
      transition:fly="{{ x: -1000, duration: 300, easing: backInOut }}"
    >
      Jenny Yang
    </h1>
  {/if}
</section>

<style>
  /* texts */
  h1 {
    position: absolute;
    font-size: 3rem;
    line-height: 1.2;
    top: 19vh;
    /* transition: transform 0.3s ease; */
  }

  section {
    position: relative;
    grid-area: additional;
    justify-self: end;
  }

  /* images */

  .left-face {
    width: 35vw;
    max-width: 233px;
  }
  @media (min-width: 640px) {
    h1 {
      font-size: 4rem;
      top: 22vh;
      /* transition: transform 0.3s ease; */
    }
  }
</style>
