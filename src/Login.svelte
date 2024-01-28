<script>
  import { navigate } from 'svelte-routing';

  let username = '';

  function login() {
    if (controllo() != '') {
      alert(`Inserisci${controllo()}`);
      return;
    }

    navigate(`home/${username}`);
  }

  function controllo() {
    let alert = '';
    if (username == '') {
      alert += ' Username'
    }
    return alert;
  }
</script>

<center>
<h1>LOGIN</h1>

<div class="container">
<input bind:value={username} type="text" placeholder="Username"/>
<br>
<br>
<button on:click={login}>Login</button>
</div>
</center>