<!-- App.svelte -->
<script>
  import { Router, Link, Route } from "svelte-routing";
  import Home from "./routes/Home.svelte";
  import Contact from "./routes/Contact.svelte";

  export let url = "";
</script>

<Router url="{url}">
    <div>
        <Route path="contact" component="{Contact}" />
        <Route path="/"><Home /></Route>
    </div>
</Router>