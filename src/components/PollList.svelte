<script>
  import { onDestroy } from "svelte";
  import PollStore from "../stores/PollStore";
  import PollDetails from "./PollDetails.svelte";

  export let polls = [];

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
    <PollDetails {poll} on:vote />
  {/each}
</div>

<style>
  .poll-list {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;
  }
</style>
