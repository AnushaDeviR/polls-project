<script>
  import Card from "../reuseable/Card.svelte";
  export let poll = [];

  //   reactive values:
  $: totalValues = poll.votesA + poll.votesB;
</script>

<Card>
  <div class="poll">
    <h3>{poll.question}</h3>
    <p>Total votes: {totalValues}</p>
    <div class="answer">
      <div class="percent percent-a">
        <span>{poll.answerA} ({poll.votesA})</span>
      </div>
    </div>
    <div class="answer">
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
