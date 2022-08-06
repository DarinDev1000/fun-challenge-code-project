<script>
  import { onMount } from "svelte";
  import { goto } from "$app/navigation";

  let selection = -1;
  let errorText = "";
  let submitText = "Submit";
  let timeExpired = false;

  // Change these per page
  let nextRoute = "step2";
  let question = "Now this is a hard one, are there any blasters in our family?";
  let answers = ["Yes", "No"];
  let correctAnswer = "Yes";

  function handleSubmit() {
    if (answers[selection] === correctAnswer && !timeExpired) {
      goto(`/${nextRoute}`, { replaceState: false });
    } else {
      errorText = "You sure about that?";
    }
  }

  function addMinutes(date, minutes) {
    return new Date(date.getTime() + minutes*60000);
  }
  onMount(() => {
    // Set the date we're counting down to
    let countDownDate = addMinutes(new Date(), 0.5).getTime();

    // Update the count down every 1 second
    let x = setInterval(function () {
      // Get today's date and time
      let now = new Date().getTime();

      // Find the distance between now and the count down date
      let distance = countDownDate - now;

      // Time calculations for days, hours, minutes and seconds
      let days = Math.floor(distance / (1000 * 60 * 60 * 24));
      let hours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
      let minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
      let seconds = ('0' + Math.floor((distance % (1000 * 60)) / 1000)).slice(-2);
      let milliseconds = ('0' + Math.floor((distance % (1000)) / 10)).slice(-2);

      // Display the result in the element with id="demo"
      document.getElementById("countdown-timer").innerHTML = `${minutes}m ${seconds}s ${milliseconds}ms`;

      // If the count down is finished, write some text
      if (distance < 0) {
        clearInterval(x);
        document.getElementById("countdown-timer").innerHTML = "EXPIRED";
        timeExpired = true;
      }
    }, 10);
  });
</script>

<div id="app" class="flex-container">
  <div class="row">
    <h1 id="countdown-timer">0m 00s 00ms</h1>
    <h2>{question}</h2>
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
    <a id="submit" class="button" on:click={handleSubmit}>{submitText}</a>
  </div>
</div>
