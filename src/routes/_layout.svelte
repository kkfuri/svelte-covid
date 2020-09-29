<style>
  main {
    position: relative;
    max-width: 112em;
    background-color: white;
    padding: 2em;
    margin: 0 auto;
    box-sizing: border-box;
    min-height: calc(100vh - 72px);
  }

  footer {
    height: 72px;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #ededed;
    text-align: center;
  }

  h6 {
    font-size: 1.6em;
    font-family: monospace;
    margin: 0;
  }
  a {
    font-size: 1.4em;
    color: #333;
    display: inline-block;
    text-decoration: none;
    transition: transform 0.4s;
    color: mediumseagreen;
  }

  a:hover {
    color: seagreen;
    transform: translateY(-4px);
  }

  .github {
    position: absolute;
    right: 2em;
    z-index: 10;
  }
</style>

<div style="min-height: 100vh">
  <main>
    <div class="github">
      <a
        target="_blank"
        rel="noopener"
        href="https://github.com/kkfuri/svelte-covid"
        aria-label="Ir para o github do projeto">
        projeto no github
      </a>
    </div>
    <slot />
  </main>
  <footer>
    <h6>
      Made by
      <a
        target="_blank"
        rel="noopener"
        href="https://github.com/kkfuri"
        aria-label="Ir para o github do desenvolvedor">
        Diego
      </a>
      with
      <a
        target="_blank"
        rel="noopener"
        href="https://sapper.svelte.dev/"
        aria-label="Ir para página do Sapper">
        Sapper
      </a>
    </h6>
  </footer>
</div>
