<script>
  import Header from "../../../lib/assets/Header.svelte";

  let bookTitle = "";
</script>

<main>
  <Header />
<div class="div1">
  <div class="div2">
    <select bind:value={bookTitle} id="bookTitle">
      <option>Book 1</option>
      <option>Book 2</option>
    </select><br />
    <label for="pagesFrom">From:</label>
    <input type="number" id="pagesFrom" /><br />
    <label for="pagesTo">To:</label>
    <input type="number" id="pagesTo" /><br />
    <label for="markAsFinished">Mark as Finished</label>
    <input type="checkbox" id="markAsFinished" />
    <button>Submit</button>
  </div>
  </div>
</main>

