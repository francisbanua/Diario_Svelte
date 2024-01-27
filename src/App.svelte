<script>
  import { Route, Router } from 'svelte-routing';
  import Home from './Home.svelte';
  import Nuovo from './Nuovo.svelte';
  import Modifica from './Modifica.svelte';
  import Visualizza from './Visualizza.svelte';
  import Login from './Login.svelte';
</script>

<Router>
  <Route path="/home/:username" component={Home} />
  <Route path="/" component={Login} />
  <Route path="/nuovo/:username" component={Nuovo} />
  <Route path="/modifica/:username/:id" component={Modifica} />
  <Route path="/visualizza/:username/:id" component={Visualizza} />
</Router>
