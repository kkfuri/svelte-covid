<script>
  export let state;
  export let cases;
  export let deaths;
  export let uf;
</script>

<style>
  article {
    font-family: "Jost", sans-serif;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    box-sizing: border-box;
    height: 142px;
    border: 2px solid #ccc;
    padding: 16px 8px;
    background: #fff;
  }
  h2 {
    white-space: nowrap;
    margin: 0 20px 0 0;
  }

  header {
    display: flex;
    align-items: center;
    margin-bottom: 16px;
  }

  h5,
  h6 {
    font-size: 16px;
    line-height: 1rem;
  }

  h6 strong,
  h5 strong {
    line-height: 1rem;
    vertical-align: middle;
    font-family: Arial, Helvetica, sans-serif;
  }

  .img-wrapper {
    border: 1px solid #ccc;
    height: 30px;
  }
</style>

<article>
  <header>
    <h2>{state}</h2>
    <div class="img-wrapper">
      <img
        width={45}
        height={30}
        alt={state}
        src="https://devarthurribeiro.github.io/covid19-brazil-api/static/flags/{uf}.png" />
    </div>
  </header>
  {#if cases}
    <h5>
      Casos confirmados:
      <strong>{cases}</strong>
    </h5>
  {/if}
  {#if deaths}
    <h6>
      Mortes:
      <strong>{deaths}</strong>
    </h6>
  {/if}
</article>
