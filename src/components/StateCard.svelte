<script>
  export let state;
  export let cases;
  export let deaths;
  export let uf;
  export let featured;
</script>

<style>
  article {
    font-family: "Jost", sans-serif;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    box-sizing: border-box;
    border: 2px solid #ccc;
    padding: 16px 8px;
    background: #fff;
    transition: border-color 0.4s;
  }

  h2 {
    white-space: nowrap;
    margin: 0 20px 0 0;
  }

  header {
    display: flex;
    align-items: center;
    margin-bottom: 1.6em;
  }

  h2 {
    font-size: 1.8em;
  }

  h5,
  h6 {
    font-size: 1.6em;
    line-height: 1.6em;
    margin: 0;
  }

  h6 strong,
  h5 strong {
    line-height: 1.6em;
    vertical-align: middle;
    font-family: Arial, Helvetica, sans-serif;
  }

  .img-wrapper {
    border: 1px solid #ccc;
    height: 30px;
  }

  article#featured {
    border: 2px solid mediumseagreen;
    padding: 48px 8px;
  }

  #featured .img-wrapper {
    border: 1px solid #ccc;
    border-radius: 2px;
    height: 24px;
  }

  #featured h5,
  #featured h6 {
    font-size: 1.8em;
  }

  #featured img {
    width: auto;
    height: 24px;
  }

  #featured h2 {
    font-size: 2em;
  }

  @media (min-width: 767px) {
    #featured .img-wrapper {
      border: 1px solid #ccc;
      border-radius: 2px;
      height: 48px;
    }
    #featured img {
      width: auto;
      height: 48px;
    }

    #featured h5,
    #featured h6 {
      font-size: 2.2em;
    }

    #featured h2 {
      font-size: 2.6em;
    }
  }
</style>

<article id={featured && 'featured'}>
  <header>
    <h2>{state}</h2>
    <div class="img-wrapper">
      <img
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
