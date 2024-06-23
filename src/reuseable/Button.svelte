<script>
  export let buttonType = "primary";
  export let flat = false;
  export let inverse = false;
</script>

<button class={buttonType} class:flat class:inverse on:click>
  <slot></slot>
</button>

<style>
  button {
    border: 0px;
    cursor: pointer;
    border-radius: 6px;
    padding: 8px 12px;
    box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.2);
  }

  .primary {
    background-color: orangered;
    color: white;
  }
  .secondary {
    background-color: #ffbe0b;
    color: white;
  }
  .flat {
    box-shadow: none;
  }
  .primary.inverse {
    color: orangered;
    background: white;
    border: 2px solid orangered;
  }
  .secondary.inverse {
    color: #ffbe0b;
    background: white;
    border: 2px solid #ffbe0b;
  }
</style>
