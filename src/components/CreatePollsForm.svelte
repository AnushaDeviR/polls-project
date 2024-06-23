<script>
  import PollStore from "../stores/PollStore.js";
  import { createEventDispatcher } from "svelte";
  import Button from "../reuseable/Button.svelte";

  let dispatch = createEventDispatcher();

  let fields = { question: "", answerA: "", answerB: "" };
  let errors = { question: "", answerA: "", answerB: "" };

  const submitHandler = () => {
    let isValid = true;

    // Validate question
    if (fields.question.trim().length < 5) {
      isValid = false;
      errors.question = "Questions must be at least 5 characters long.";
    } else {
      errors.question = "";
    }

    // Validate answer A
    if (fields.answerA.trim().length < 1) {
      isValid = false;
      errors.answerA = "Answer A cannot be empty.";
    } else {
      errors.answerA = "";
    }

    // Validate answer B
    if (fields.answerB.trim().length < 1) {
      isValid = false;
      errors.answerB = "Answer B cannot be empty.";
    } else {
      errors.answerB = "";
    }

    // adds new poll
    if (isValid) {
      let poll = { ...fields, votesA: 0, votesB: 0, id: Math.random() };
      PollStore.update((currentPolls) => {
        return [poll, ...currentPolls];
      });
      // add is dispatches to App component
      dispatch("add");
    }
  };
</script>

<form on:submit|preventDefault={submitHandler}>
  <div class="form-fields">
    <label for="question"> Poll Question: </label>
    <input type="text" id="question" bind:value={fields.question} />
    <div class="errorMsg">{errors.question}</div>
  </div>

  <div class="form-fields">
    <label for="answer-a"> Answer A: </label>
    <input type="text" id="answer-a" bind:value={fields.answerA} />
    <div class="errorMsg">{errors.answerA}</div>
  </div>

  <div class="form-fields">
    <label for="answer-b"> Answer B: </label>
    <input type="text" id="answer-b" bind:value={fields.answerB} />
    <div class="errorMsg">{errors.answerB}</div>
  </div>

  <Button>Add Poll</Button>
</form>

<style>
  form {
    width: 400px;
    margin: 0 auto;
    text-align: center;
  }

  .form-fields {
    margin: 18px auto;
  }

  input {
    width: 100%;
    border-radius: 6px;
  }

  label {
    margin: 10px auto;
    text-align: left;
  }
  .errorMsg {
    color: red;
    text-align: left;
    font-style: italic;
    font-size: 12px;
  }
</style>
