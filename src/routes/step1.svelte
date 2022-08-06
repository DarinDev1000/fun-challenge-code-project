<script>
  import { goto } from '$app/navigation';

  let selection = -1;
  let errorText = '';
  let submitText = 'Submit';

  // Change these per page
  let route = 'step2';
  let question = 'Now this is a hard one, are there any blasters in our family?';
  let answers = [
    'Yes',
    'No'
  ];
  let correctAnswer = 'Yes';

  function handleSubmit() {
    if (answers[selection] === correctAnswer) {
      goto(`/${route}`, { replaceState: false })
    } else {
      errorText = 'You sure about that?';
    }
  }
</script>

<div id='app' class='flex-container'>
  <div class='row'>
    <h2>{question}</h2>
  </div>
  {#each answers as answer, i}
    <div class='row'>
      <label>
        <input type='radio' class='radio-button' bind:group={selection} value={i} />
        {answer}
      </label>
    </div>
  {/each}
  <div class='row'>
    <p>{errorText}</p>
    <a id='submit' class='button' on:click={handleSubmit}>{submitText}</a>
  </div>
</div>
