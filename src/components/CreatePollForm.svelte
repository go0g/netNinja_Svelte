<script>
  import {createEventDispatcher} from 'svelte';
  import Button from "../shared/Button.svelte";

  let dispatcher = createEventDispatcher();

  let fields = {
    question: "",
    answerA: "",
    answerB: ""
  };
  let errors = {
    question: "",
    answerA: "",
    answerB: ""
  };

  let valid = false;

  const submitHandler = () => {
    valid = true;

    // validate question
    if (fields.question.trim().length < 5) {
      valid = false;
      errors.question = "Bitte Frage mit mehr als 5 Zeichen eingeben!";
    } else {
      errors.question = "";
    }
    // validate AnswerA
    if (fields.answerA.trim().length < 1) {
      valid = false;
      errors.answerA = "Antwort A bitte ausfüllen";
    } else {
      errors.answerA = "";
    }
    // validate AnswerA
    if (fields.answerB.trim().length < 1) {
      valid = false;
      errors.answerB = "Antwort B bitte ausfüllen";
    } else {
      errors.answerB = "";
    }

    // ad field

    if (valid) {
      let poll = {...fields, voteA:0, voteB:0, id: Math.random()};
      dispatcher('add', poll);
      console.log(valid, fields);
    }
  };
</script>

<style>
  form {
    width: 400px;
    margin: 0 auto;
    text-align: center;
  }

  .form-field {
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

  .error {
    font-weight: bold;
    font-size: 12px;
    color: #d91b42;
  }
</style>

<form on:submit|preventDefault={submitHandler}>
  <div class="form-field">
    <label for="question">Poll Question:</label>
    <input type="text" id="question" bind:value={fields.question} />
    <div class="error">{errors.question}</div>
  </div>
  <div class="form-field">
    <label for="answer-a">Answer A:</label>
    <input type="text" id="answer-a" bind:value={fields.answerA} />
    <div class="error">{errors.answerA}</div>
  </div>
  <div class="form-field">
    <label for="answer-b">Answer B:</label>
    <input type="text" id="answer-b" bind:value={fields.answerB} />
    <div class="error">{errors.answerB}</div>
  </div>
  <Button type="secondary" flat={true} inverse={true}>Add Poll</Button>
</form>
