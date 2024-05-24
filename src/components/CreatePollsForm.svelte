<script>
  import Button from "../reuseable/Button.svelte";

  let fields = { question: "", answerA: "", answerB: "" };
  let errors = { question: "", answerA: "", answerB: "" };
  let isValid = false;

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
      errors.question = "Answer A cannot be empty.";
    } else {
      errors.question = "";
    }

    //  validate ans 2
    if (fields.answerB.trim().length < 1) {
      isValid = false;
      errors.question = "Answer B cannot be empty.";
    } else {
      errors.question = "";
    }
  };

  if (isValid) {
    console.log("valid", fields);
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
  <Button flat={true} inverse={true}>Add Poll</Button>
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
