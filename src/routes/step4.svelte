<script>
  import { goto } from "$app/navigation";

  let submitTries = 0;
  let maxSubmitTries = 5;
  let errorText = "";
  let submitText = "Submit";
  let submittedAnswer = "";

  // Change these per page
  let nextRoute = "step5";
  let question = "What is the passcode?";
  let correctAnswer = 9475;

  function handleSubmit() {
    if (submittedAnswer === correctAnswer && submitTries < maxSubmitTries) {
      goto(`/${nextRoute}`, { replaceState: false });
    } else {
      submitTries++;
      errorText = "You sure about that?";
    }
  }
</script>

<div id="app" class="flex-container">
  <div class="row">
    <h2>{question}</h2>
  </div>
    <div class="row">
      <label>
        <input type="number" bind:value={submittedAnswer} placeholder="enter a 4 number passcode" />
      </label>
    </div>
  <div class="row">
    <p>{errorText}</p>
    <a id="submit" class="button" on:click={handleSubmit}>{submitText}:
      {#if maxSubmitTries-submitTries>1 && submitTries!==0}{maxSubmitTries - submitTries} more tries{/if}
      {#if maxSubmitTries-submitTries===1}{maxSubmitTries - submitTries} more try!{/if}
      {#if maxSubmitTries-submitTries<=0}No tries!{/if}
    </a>
  </div>
</div>
