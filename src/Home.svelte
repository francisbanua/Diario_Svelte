<script>
  import {navigate} from 'svelte-routing';

  export let username;

  let entries = JSON.parse(localStorage.getItem('diaryEntries' + username)) || [];
  entries.sort((a,b)=>new Date(b.data)-new Date(a.data));

  let cerca='';

  function nuovoEntry() {
    navigate(`/nuovo/${username}`);
  }

  function modificaEntry(id) {
    navigate(`/modifica/${username}/${id}`);
  }

  function eliminaEntry(id) {
    entries = entries.filter(entry => entry.id !== id);
    localStorage.setItem(`diaryEntries${username}`, JSON.stringify(entries));
  }

  function visualizzaEntry(id) {
    navigate(`/visualizza/${username}/${id}`);
  }

  function ricerca(){
    entries = JSON.parse(localStorage.getItem(`diaryEntries${username}`)) || [];
    if(cerca!=''){
     entries = entries.filter(entry => entry.titolo.toLowerCase().includes(cerca.toLowerCase())===true);
    }
  }

  function logout() {
    navigate('/');
  }
</script>

<center>
<h1>{username}'s Home</h1>

<button on:click={logout}>Logout</button>
<br>
<br>
<div class="container">
<button on:click={nuovoEntry}>Nuovo</button>
<input bind:value={cerca} type=text placeholder="Cerca">
<button on:click={ricerca}>Cerca</button>
</div>

<br>

<div class="container">
{#if entries.length > 0}
  <table>
    <thead>
        <th>Titolo</th>
        <th>Data</th>
        <th>Modifica</th>
        <th>Elimina</th>
    </thead>
    <tbody>
      {#each entries as entry}
        <tr>
          <td  on:click={() => visualizzaEntry(entry.id)}><strong>{entry.titolo}</strong></td>
          <td  on:click={() => visualizzaEntry(entry.id)}>{entry.data}</td>
          <td on:click={() => modificaEntry(entry.id)} class="symbol" id="modifica">o</td>
          <td on:click={() => eliminaEntry(entry.id)} class="symbol" id="elimina">k</td>
        </tr>
      {/each}
    </tbody>
  </table>
{:else}
  <h3>:(</h3>
  <p>Clicca su 'Nuovo' per iniziare</p>
{/if}
</div>
</center>