<script>
  import {navigate } from 'svelte-routing';

  export let id;
  export let username;

  let titolo = '';
  let data = '';
  let testo = '';

  let entries = JSON.parse(localStorage.getItem(`diaryEntries${username}`)) || [];
  let modificaEntry = entries.find(entry => entry.id == id);

  titolo = modificaEntry.titolo;
  data = modificaEntry.data;
  testo = modificaEntry.testo;

  function home() {
    navigate(`/home/${username}`);
  }

  function conferma() {
    if (controllo() != '') {
      alert(`Inserisci${controllo()}`);
      return;
    }
    
    let entriesModificati = entries.map(entry => {
      if (entry.id == id) {
        return {
          ...entry,
          titolo,
          data,
          testo,
        };
      }
      return entry;
    });

    localStorage.setItem(`diaryEntries${username}`, JSON.stringify(entriesModificati));
    
    home()
  }

  function controllo() {
    let alert = '';
    if (titolo == '') {
      alert += ' Titolo'
    }
    if (data == '') {
      alert += ' Data'
    }
    if (testo == '') {
      alert += ' Testo'
    }
    return alert;
  }

</script>

<h1>Modifica</h1>
<center><div class="container">
<button on:click={home}>Home</button>
<br>
<br>
<input bind:value={titolo} type="text" placeholder="Titolo">
<input bind:value={data} type="date" >
<br>
<br>
<textarea bind:value={testo} placeholder="Testo"></textarea>
<br>
<br>
<button on:click={conferma}>Conferma modifica</button>
</div></center>