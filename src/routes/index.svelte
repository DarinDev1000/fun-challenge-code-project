<script>
  let proceedText = 'Proceed';
  setInterval(() => {
    switch (proceedText) {
      case 'Proceed':
        proceedText = 'Proceed.';
        break;
      case 'Proceed.':
        proceedText = 'Proceed..';
        break;
      case 'Proceed..':
        proceedText = 'Proceed...';
        break;
      case 'Proceed...':
        proceedText = 'Proceed';
        break;
      }
    }, 1000);
</script>

<div id='app' class='flex-container'>
  <div class='row'>
    <h1>You have arrived at C³</h1>
    <h3>Crawmer Cypher Challenge</h3>
  </div>
  <div class='row'>
    <a id='proceed' href='/step1' class='button'>{proceedText}</a>
  </div>
</div>
