<script>
  import { setContext } from "svelte"
  import { Router } from "@roxi/routify"
  import { routes } from "../.routify/routes"
  import { writable } from "svelte/store"

  setContext("hashElements", new Map());

</script>

<!-- src/App.svelte -->
<Router {routes} />
