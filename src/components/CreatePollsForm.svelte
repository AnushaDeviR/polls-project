<script>
  import Button from "../reuseable/Button.svelte";
  import { createEventDispatcher } from "svelte";

  let fields = { question: "", answerA: "", answerB: "" };
  let errors = { question: "", answerA: "", answerB: "" };
  let isValid = false;

  let dispatch = createEventDispatcher();

  const submitHandler = () => {
    isValid = true;

    //  validate question
    if (fields.question.trim().length < 5) {
      // question should at least be 5 characters long
      isValid = false;
      errors.question = "Questions must be at least 5 characters long.";
    } else {
      errors.question = "";
    }

    // validate answer 1
    if (fields.answerA.trim().length < 1) {
      isValid = false;
      errors.answerA = "Answer A cannot be empty.";
    } else {
      errors.answerA = "";
    }

    //  validate ans 2
    if (fields.answerB.trim().length < 1) {
      isValid = false;
      errors.answerB = "Answer B cannot be empty.";
    } else {
      errors.answerB = "";
    }
  };

  if (isValid) {
    let poll = { ...fields, votesA: 0, votesB: 0, id: Math.random() };
    dispatch("add", poll);
  }
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

  <!-- FIXME: Broken button? -->
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
