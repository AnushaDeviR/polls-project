<script>
  import PollDetails from "./PollDetails.svelte";

  export let polls = [];
</script>

<div class="poll-list">
  <!-- NOTE: poll.id is the key -->
  {#each polls as poll (poll.id)}
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
