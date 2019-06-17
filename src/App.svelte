<script>
  let name = "";
  let loading = false;
  const apiKey = "m7NZGH33sHzM9WLEheMewhyoRSrjEsGN";
  const url = `https://api.giphy.com/v1/gifs/search?api_key=${apiKey}`;
  let gifs = [];
  let disabled = false;
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
  * {
    padding: 0;
    margin: 0;
    box-sizing: border-box;
  }
  ul {
    padding: 0;
  }
  li {
    list-style-type: none;
  }
  .form-control {
    text-align: center;
    margin-top: 25px;
  }
  .form-control input {
    padding: 10px;
    border-radius: 3px;
  }
  .form-control button {
    padding: 10px;
  }
  .container {
    max-width: 1000px;
    margin: 100px auto;
  }
  .list {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    grid-gap: 5px;
    grid-auto-flow: dense;
  }
  .result-img {
    width: 100%;
    height: 100%;
    border-radius: 5px;
  }
</style>

<form on:submit={formSubmitted} class="form-control">
  <label for="search">Search</label>
  <input bind:value={name} type="text" placeholder="search term" />
  <button type="submit">Submit</button>
</form>
<div class="container">

  {#if loading}
    <h1>loading...</h1>
  {/if}
  <ul class="list">
    {#each gifs as gif, i}
      <li>
        <img src={gif.images.fixed_height.url} alt="gif" class="result-img" />
      </li>
    {/each}
  </ul>
</div>
