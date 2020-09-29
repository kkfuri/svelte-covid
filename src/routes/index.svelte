<script>
  import StateCard from "../components/StateCard.svelte";
  import Skeleton from "../components/Skeleton.svelte";
  import { onMount, onDestroy } from "svelte";
  import { fade, fly } from "svelte/transition";

  const skeletonItems = 8;

  let loading = false;
  let data = [];
  let filteredItems = [];
  let inputValue;
  let inputRef;
  let active = null;

  function update(event) {
    active = document.activeElement;
  }

  function normalize(str) {
    return str
      .normalize("NFD")
      .replace(/[\u0300-\u036f]/g, "")
      .toUpperCase()
      .trim();
  }

  $: {
    filteredItems = inputValue
      ? data.filter(
          i =>
            normalize(i.state).includes(normalize(inputValue)) ||
            normalize(i.uf).includes(normalize(inputValue))
        )
      : data;
  }

  onMount(() => {
    getDados();
  });

  async function getDados() {
    loading = true;
    const res = await fetch("https://covid19-brazil-api.now.sh/api/report/v1");
    const json = await res.json();
    data = json.data;
    loading = false;
  }

  function handleKeydown(event) {
    if (event.key === "Escape") inputRef.focus();
  }
</script>

<style>
  h3 {
    font-family: "Jost", sans-serif;
    font-weight: 900;
    text-align: center;
    margin: 16px 0;
    font-size: 5.2em;
  }
  .grid {
    display: grid;
    grid-template-columns: repeat(1, minmax(0, 1fr));
    gap: 16px;
    margin: 0 auto;
  }

  @media (min-width: 767px) {
    h3 {
      font-size: 6.4em;
    }
    .grid {
      grid-template-columns: repeat(2, minmax(0, 1fr));
    }
  }

  #input span {
    display: none;
  }

  #input {
    position: relative;
  }

  #input input:focus {
    padding: 12px 24px;
    outline: 0;
    border: 2px solid mediumseagreen;
  }

  #input input {
    transition: padding 0.4s;
    box-sizing: border-box;
    border: 2px solid #ccc;
    margin: 12px 0;
    padding: 12px 24px;
    font-size: 1.8em;
    width: 100%;
  }
  h5 {
    font-family: "Jost", sans-serif;
    font-weight: 900;
    text-align: center;
    font-size: 2.4em;
  }

  @media (min-width: 1024px) {
    #input input {
      padding: 12px 5rem;
    }
    #input span {
      display: inline;
      background-color: #efefef;
      border-radius: 6px;
      padding: 2px 8px;
      position: absolute;
      font-size: 1.2em;
      left: 10px;
      top: 24px;
    }
    .grid {
      grid-template-columns: repeat(3, minmax(0, 1fr));
    }
  }

  a {
    border: 0;
    text-decoration: none;
    transition: 0.2s;
  }

  a:hover {
    transform: scale(1.05);
  }

  a:hover :global(article) {
    border: 2px solid mediumseagreen;
  }
</style>

<svelte:head>
  <title>Covid no Brasil</title>
</svelte:head>

<svelte:window on:keydown={handleKeydown} on />

<h3>Covid no Brasil</h3>
{#if !loading}
  <div id="input">
    <input
      type="text"
      bind:value={inputValue}
      bind:this={inputRef}
      on:focus={update}
      on:blur={update}
      placeholder="Pesquisar por estado brasileiro" />
    {#if inputRef !== active}
      <span transition:fade|local>esc</span>
    {/if}
  </div>
{/if}
<div class="grid">
  {#if filteredItems.length > 0 && !loading}
    {#each filteredItems as states (states.uid)}
      <a
        href={`/${states.uf}`}
        aria-label={`Ir para página do estado ${states.uf}`}
        transition:fade|local>
        <StateCard {...states} />
      </a>
    {/each}
  {/if}
  {#if loading}
    {#each [...new Array(skeletonItems)] as states}
      <div transition:fade|local>
        <Skeleton />
      </div>
    {/each}
  {/if}
</div>
{#if filteredItems.length === 0 && !loading}
  <h5>Nenhum estado encontrado</h5>
{/if}
