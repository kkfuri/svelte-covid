<script context="module">
  export function preload({ params }) {
    const { uf } = params;
    return { uf };
  }
</script>

<script>
  import { onMount } from "svelte";
  import StateCard from "../components/StateCard.svelte";
  import Skeleton from "../components/Skeleton.svelte";
  export let uf;

  let loading = false;
  let result = null;

  onMount(() => {
    getDados();
  });

  async function getDados() {
    loading = true;
    const res = await fetch(
      `https://covid19-brazil-api.now.sh/api/report/v1/brazil/uf/${uf}`
    );
    result = await res.json();
    loading = false;
  }
</script>

<svelte:head>
  <title>{result ? result.state : 'Estado do Brasil'}</title>
</svelte:head>

<a href="/">Voltar</a>

{#if result && !loading}
  <div style="max-width: 320px; margin: 0 auto">
    <StateCard {...result} />
  </div>
{/if}

{#if loading}
  <div style="max-width: 320px; margin: 0 auto">
    <Skeleton />
  </div>
{/if}
