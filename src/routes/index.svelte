<script>
  import StateCard from "../components/StateCard.svelte";
  import Skeleton from "../components/Skeleton.svelte";
  import { onMount } from "svelte";
  let loading = false;
  let result = [];

  onMount(() => {
    getDados();
  });

  async function getDados() {
    loading = true;
    const res = await fetch("https://covid19-brazil-api.now.sh/api/report/v1");
    const json = await res.json();
    result = json.data;
    loading = false;
  }
</script>

<style>
  h3 {
    font-family: "Jost", sans-serif;
    font-weight: 900;
    text-align: center;
    margin: 16px 0;
    font-size: 64px;
  }
  .grid {
    display: grid;
    grid-template-columns: repeat(3, minmax(0, 1fr));
    gap: 16px;
  }

  @media (max-width: 1024px) {
    .grid {
      grid-template-columns: repeat(1, minmax(0, 1fr));
    }
  }
</style>

<svelte:head>
  <title>Home</title>
</svelte:head>

<h3>Covid no Brasil</h3>
<div class="grid">
  {#if result.length > 0 && !loading}
    {#each result as data (data.uid)}
      <StateCard {...data} />
    {/each}
  {/if}
  {#if loading}
    {#each [...new Array(8)] as data}
      <Skeleton />
    {/each}
  {/if}
</div>
