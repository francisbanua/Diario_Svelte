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

<h1>LOGIN</h1>

<center><div class="container">
<input bind:value={username} type="text" placeholder="Username"/>
<br>
<br>
<button on:click={login}>Login</button>
</div></center>