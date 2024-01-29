<script>
  import {navigate} from 'svelte-routing';

  export let username

  let titolo = '';
  let data = '';
  let testo = '';

  function home() {
    navigate(`/home/${username}`);
  }

  function conferma() {
    if (controllo() != '') {
      alert(`Inserisci${controllo()}`);
      return;
    }

    const entry = {
      id: Date.now(),
      titolo,
      data,
      testo,
    };

    let entries = JSON.parse(localStorage.getItem(`diaryEntries${username}`)) || [];
    entries.push(entry);
    localStorage.setItem(`diaryEntries${username}`, JSON.stringify(entries));

    home();
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

<center>
<h1>Nuovo</h1>
<div class="container">
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
<button on:click={conferma}>Conferma aggiunta</button>
</div>
</center>