<script>
  import Header from './components/Header.svelte'
  import Window from './components/Window.svelte'
</script>

<main>
  <div class='app'>
    <Header />
    <Window />
  </div>
</main>

<style lang="scss">
  $white: rgb(255, 255, 255);

  body {
    color: $white;
    overflow-y: hidden;
  }

  main {
    height: 100%;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  .app {
    display: grid;
    grid-template-rows: minmax(min-content, max-content) auto;
    align-items: stretch;
    justify-content: stretch;
    height: 100%;
    width: 100%;
  }
</style>
