<script>
  // import { fly, fade } from "svelte/transition";
  // import { sineInOut } from "svelte/easing";
  import { main, menuOpen, skillPage, projectPage } from "../../stores.js";
</script>

<div class="direct-btns">
  <slot />
</div>

<style>
  .direct-btns {
    font-size: 19px;
  }
</style>
