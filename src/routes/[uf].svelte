<script context="module">
  export async function preload({ params }) {
    const { uf } = params;
    const res = await this.fetch(
      `https://covid19-brazil-api.now.sh/api/report/v1/brazil/uf/${uf}`
    );
    const result = await res.json();
    return { result };
  }
</script>

<script>
  import { onMount } from "svelte";
  import { goto } from "@sapper/app";
  import StateCard from "../components/StateCard.svelte";
  import Skeleton from "../components/Skeleton.svelte";
  export let result;

  onMount(() => {
    if (result.error) goto("/");
  });
</script>

<style>
  div {
    margin: 4rem auto;
    max-width: 480px;
  }
  a {
    transition: 0.4s;
  }
  a:hover {
    color: mediumseagreen;
  }
</style>

<svelte:head>
  <title>{result ? result.state : 'Estado do Brasil'}</title>
</svelte:head>

<a href="/">Voltar</a>

{#if !result.error}
  <div>
    <StateCard {...result} featured />
  </div>
{/if}
