<script>
  import Dashboard from "./components/Dashboard.svelte";
  import Panel from "./components/Panel.svelte";
  import { onMount } from "svelte";

  let data;

  onMount(async () => {
    const res = await fetch(
      "https://api.coindesk.com/v1/bpi/historical/close.json"
    );
    data = await res.json();
  });
</script>

<main>
  {#if data}
    <Panel />
    <Dashboard data={data.bpi} />
    <Panel />
  {/if}
</main>

<style>
  :global(body) {
    margin: 0;
    padding: 0;
    min-height: 100vh;
  }

  main {
    display: flex;
    flex-direction: column;
    width: 100%;
    min-height: 100vh;
    text-rendering: optimizeSpeed;
    line-height: 1.5;
  }

  main {
    margin: 0 auto;
  }

  @media (min-width: 320px) {
    main {
      max-width: none;
    }
  }
</style>
