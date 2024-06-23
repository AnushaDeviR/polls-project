<script>
  import { fade, slide, scale } from "svelte/transition";
  import { flip } from "svelte/animate";
  import PollStore from "../stores/PollStore.js";
  import PollDetails from "./PollDetails.svelte";

  /*
  NOTE: METHOD 1- this is re-fired whenever the data is changed
    const unsub = PollStore.subscribe((data) => {
      polls = data;
    });

    onDestroy(() => {
      unsub();
    });
  */
</script>

<div class="poll-list">
  <!-- NOTE: poll.id is the key -->
  <!-- NOTE: METHOD 2- easier way to subscribe and unsubscribe to stores: $PollStore
 -->
  {#each $PollStore as poll (poll.id)}
    <!-- NOTE: transitions, animations cannot be added to custom components but to only html elements -->
    <div in:fade out:scale|local animate:flip={{ duration: 500 }}>
      <PollDetails {poll} />
    </div>
  {/each}
</div>

<style>
  .poll-list {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;
  }
</style>
