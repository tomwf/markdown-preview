<script>
  import { marked } from 'marked'
  import FaRegEye from 'svelte-icons/fa/FaRegEye.svelte'

  function handleInput(e) {
    markdown = e.target.value
  }

  function toggleFullscreen() {
    const preview = document.querySelector('.preview')

    isFullscreen = !isFullscreen

    if (isFullscreen) {
      preview.classList.add('fullscreen')
    } else {
      preview.classList.remove('fullscreen')
    }
  }

  let markdown = ""
  let isFullscreen = false
</script>

<div class="window__container">
  <div id="markdown" class="window">
    <div class="window__title">
      <p>Markdown</p>
      <div class="toggle-fullscreen">
        <div class="toggle-fullscreen__icon">
          <FaRegEye />
        </div>
        <button class="toggle-fullscreen__btn" on:click={toggleFullscreen}></button>
      </div>
    </div>

    <div class="window__content markdown">
      <textarea on:input={handleInput}></textarea>
    </div>
  </div>

  <div class:fullscreen="{isFullscreen}" class="window preview">
    <div class="window__title">
      <p>Preview</p>
      <div class="toggle-fullscreen">
        <div class="toggle-fullscreen__icon">
          <FaRegEye />
        </div>
        <button class="toggle-fullscreen__btn" on:click={toggleFullscreen}></button>
      </div>
    </div>

    <div id="preview" class="window__content">
        {@html marked(markdown)}
    </div>
  </div>
</div>

<style lang="scss">
  $gray: rgb(27, 29, 32);
  $dark-gray: rgb(21, 22, 25);
  $light-gray: rgb(44, 45, 48);

  .window {
    display: grid;
    grid-template-rows: minmax(min-content, max-content) auto;
    align-items: stretch;
    height: 100%;

    &__container {
      position: relative;
    }

    &__title {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 0 1em;
      background-color: $gray;
      height: 50px;
      font-family: sans-serif;
      text-transform: uppercase;
    }

    &__content, &__content.markdown > textarea {
      background-color: $dark-gray;

      &:focus {
        outline: none;
      }
    }

    &__content {
      overflow: auto;
      padding-left: 1em;

      &.markdown {
        position: relative;

        & > textarea {
          padding: 0;
          display: block;
          width: 100%;
          height: 100%;
          resize: none;
          border: none;
          color: inherit;
          margin: 0;
          font-family: monospace;
        }
      }
    }
  }

  .toggle-fullscreen {
    position: relative;
    display: block;
    width: 20px;
    height: 20px;

    &__icon {
      transform: translateY(10%);
    }

    &__btn {
      position: absolute;
      background: none;
      border: none;
      cursor: pointer;
      display: block;
      top: 0;
      left: 0;
      width: 20px;
      height: 20px;

      &:active {
        background: none;
      }
    }
  }

  .preview {
    visibility: hidden;
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;

    &.fullscreen {
      position: absolute;
      visibility: visible;
      width: 100%;
    }

    & > .window__content {
      padding-right: 1em;
      font-family: 'Roboto Serif', serif;
    }
  }

  @media (min-width: 500px) {
    .window {
      position: initial;
      width: 50vw;

      &__container {
        display: grid;
        align-items: stretch;
        grid-template-columns: repeat(2, 1fr);
      }
    }

    #markdown {
      border-right: 4px solid $light-gray;

      & .toggle-fullscreen {
        visibility: hidden;
      }
    }

    .preview {
      visibility: visible;
    }
  }
</style>
