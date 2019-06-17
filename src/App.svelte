<script>
  let name = "";
  let loading = false;
  const apiKey = "m7NZGH33sHzM9WLEheMewhyoRSrjEsGN";
  const url = `https://api.giphy.com/v1/gifs/search?api_key=${apiKey}`;
  let gifs = [];
  function formSubmitted(event) {
    event.preventDefault();

    return fetch(`${url}&q=${name}`)
      .then(data => {
        loading = true;
        return data.json();
      })

      .then(({ data }) => {
        gifs = data;
        loading = false;
      });
  }
</script>

<style>

</style>

<form on:submit={formSubmitted}>
  <label for="search">Search</label>
  <input bind:value={name} type="text" placeholder="search term" />
  <button type="submit">Submit</button>
</form>
<p>{name || 'Andrew'} </p>
{#if loading}
  <h1>loading...</h1>
{/if}
<div class="container" />
