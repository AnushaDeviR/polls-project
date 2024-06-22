<script>
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  export let tabList;
  export let activeTab;
</script>

<div class="Tab">
  <ul>
    {#each tabList as tab}
      <!-- svelte-ignore a11y-click-events-have-key-events -->
      <li on:click={() => dispatch("handleTabChange", tab)}>
        <div class:active={tab === activeTab}>{tab}</div>
      </li>
    {/each}
  </ul>
</div>

<style>
  .Tab {
    margin-bottom: 40px;
  }
  ul {
    display: flex;
    justify-content: center;
    list-style-type: none; /* bullet point (disc) in ul*/
    padding: 0;
  }
  li {
    margin: 0 16px;
    border: 18px;
    color: #555;
    cursor: pointer;
  }
  .active {
    color: orangered;
    border-bottom: 2px solid orangered;
    padding-bottom: 8px;
  }
</style>
