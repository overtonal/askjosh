<script>
  let count = 0;

  function increment() {
    count += 1;
  }
</script>

<style>
  main {
    font-family: sans-serif;
    padding: 2rem;
    text-align: center;
  }

  button {
    padding: 0.5rem 1rem;
    font-size: 1.2rem;
    margin-top: 1rem;
    cursor: pointer;
  }
</style>

<main>
  <h1>JavaScript Test</h1>
  <p>The counter below only works if JS is running:</p>

  <h2>{count}</h2>
  <button on:click={increment}>Click Me</button>
</main>