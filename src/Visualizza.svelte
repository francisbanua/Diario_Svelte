<script>
  import {navigate } from 'svelte-routing';

  export let id;
  export let username;

  let titolo = '';
  let data = '';
  let testo = '';

  let entries = JSON.parse(localStorage.getItem(`diaryEntries${username}`));
  let visualizzaEntry = entries.find(entry => entry.id == id);

  titolo = visualizzaEntry.titolo;
  data = visualizzaEntry.data;
  testo = visualizzaEntry.testo;

  function home() {
    navigate(`/home/${username}`);
  }
</script>

<center>
<h1>Visualizza</h1>
<div class="container">
<button on:click={home}>Home</button>
<h2>{titolo}</h2>
<h4>{testo}</h4>
<p id="firma"> - {username}, {data}</p>
</div>
</center>