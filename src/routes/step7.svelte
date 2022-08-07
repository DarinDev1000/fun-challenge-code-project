<script>
  import { goto } from "$app/navigation";

  let selection = -1;
  let submitTries = 0;
  let maxSubmitTries = 4;
  let errorText = "";
  let submitText = "Submit";

  // Change these per page
  let nextRoute = "step8";
  let question = "How many BBs are in this picture?";
  let answers = ["1", "2", "3", "4", "5", "6"];
  let correctAnswer = "4";

  function handleSubmit() {
    submitTries++;
    if (answers[selection] === correctAnswer && submitTries < maxSubmitTries) {
      goto(`/${nextRoute}`, { replaceState: false });
    } else {
      errorText = "Are you sure?";
    }
  }
</script>

<div id="app" class="flex-container">
  <div class="row">
    <h2>{question}</h2>
    <img src="IMG_20200715_061700.jpg" alt="rl-rank" width="300px" height="400px">
  </div>
  {#each answers as answer, i}
    <div class="row">
      <label>
        <input type="radio" class="radio-button" bind:group={selection} value={i} />
        {answer}
      </label>
    </div>
  {/each}
  <div class="row">
    <p>{errorText}</p>
    <a id="submit" class="button" on:click={handleSubmit}>{submitText}:
      {#if maxSubmitTries-submitTries>1 && submitTries!==0}{maxSubmitTries - submitTries} more tries{/if}
      {#if maxSubmitTries-submitTries===1}{maxSubmitTries - submitTries} more try!{/if}
      {#if maxSubmitTries-submitTries<=0}No tries!{/if}
    </a>
  </div>
</div>
