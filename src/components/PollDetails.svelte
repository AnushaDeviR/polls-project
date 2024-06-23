<script>
  import { tweened } from "svelte/motion";
  import Button from "../reuseable/Button.svelte";
  import Card from "../reuseable/Card.svelte";
  import PollStore from "../stores/PollStore.js";

  export let poll = [];

  //   tweened percentages:
  const tweenedA = tweened(0);
  const tweenedB = tweened(0);

  //   reactive values:
  $: totalVotes = poll.votesA + poll.votesB;
  $: percentageA = Math.floor((100 / totalVotes) * poll.votesA) || 0;
  $: percentageB = Math.floor((100 / totalVotes) * poll.votesB) || 0;

  $: tweenedA.set(percentageA);
  $: tweenedB.set(percentageB);

  const handleVotes = (option, id) => {
    PollStore.update((currentPolls) => {
      let copiedPolls = [...currentPolls];
      // finds the poll that matches the id from the copiedPolls
      let upVotedPoll = copiedPolls.find((poll) => poll.id == id);

      if (option === "a") {
        upVotedPoll.votesA++;
      }
      if (option === "b") {
        upVotedPoll.votesB++;
      }

      return copiedPolls;
    });
  };

  const handleDelete = (id) => {
    PollStore.update((currentPolls) => {
      return currentPolls.filter((poll) => poll.id !== id);
    });
  };
</script>

<Card>
  <div class="poll">
    <h3>{poll.question}</h3>
    <p>Total votes: {totalVotes}</p>
    <!-- svelte-ignore a11y-click-events-have-key-events -->
    <div class="answer" on:click={() => handleVotes("a", poll.id)}>
      <div class="percent percent-a" style="width: {$tweenedA}%"></div>
      <span>{poll.answerA} ({poll.votesA})</span>
    </div>
    <!-- svelte-ignore a11y-click-events-have-key-events -->
    <div class="answer" on:click={() => handleVotes("b", poll.id)}>
      <div class="percent percent-b" style="width: {$tweenedB}%"></div>
      <span>{poll.answerB} ({poll.votesB})</span>
    </div>
  </div>
  <div class="delete">
    <Button flat={true} on:click={() => handleDelete(poll.id)}>Delete</Button>
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

  .percent {
    height: 100%;
    position: absolute;
    box-sizing: border-box;
  }
  .percent-a {
    background: rgb(147, 182, 182, 0.5);
    border-left: 4px solid rgb(147, 182, 182);
  }
  .percent-b {
    background: rgb(239, 212, 103, 0.5);
    border-left: 4px solid rgb(239, 212, 103);
  }

  .delete {
    margin-top: 30px;
    text-align: center;
  }
</style>
