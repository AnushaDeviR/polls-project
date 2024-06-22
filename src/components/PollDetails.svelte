<script>
  import { createEventDispatcher } from "svelte";
  import Card from "../reuseable/Card.svelte";
  export let poll = [];

  const dispatch = createEventDispatcher();

  //   reactive values:
  $: totalValues = poll.votesA + poll.votesB;

  const dispatchVotes = (option, id) => {
    dispatch("vote", { option, id });
  };
</script>

<Card>
  <div class="poll">
    <h3>{poll.question}</h3>
    <p>Total votes: {totalValues}</p>
    <!-- svelte-ignore a11y-click-events-have-key-events -->
    <div class="answer" on:click={() => dispatchVotes("a", poll.id)}>
      <div class="percent percent-a">
        <span>{poll.answerA} ({poll.votesA})</span>
      </div>
    </div>
    <!-- svelte-ignore a11y-click-events-have-key-events -->
    <div class="answer" on:click={() => dispatchVotes("b", poll.id)}>
      <div class="percent percent-b">
        <span>{poll.answerB} ({poll.votesB})</span>
      </div>
    </div>
  </div>
</Card>

<style>
  h3 {
    margin: 0 auto;
  }

  p {
    color: grey;
  }

  .answer {
    position: relative;
    background-color: #e6d7eb;
    margin: 10px auto;
    cursor: pointer;
  }

  .answer:hover {
    opacity: 0.6;
  }

  span {
    display: inline-block;
    padding: 10px 20px;
  }
</style>
