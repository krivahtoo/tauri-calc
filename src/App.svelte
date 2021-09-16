<script>
    import { appWindow } from '@tauri-apps/api/window'
    import { evaluate } from 'mathjs'
    /* import minimizeIcon from '../images/minimize.svg'
    import maximizeIcon from '../images/maximize.svg'
    import closeIcon from '../images/close.svg' */

    let result = '0';

    function close() {
      appWindow.close()
    }
    function clear() {
      result = '0'
    }
    function operator(char) {
      return function () {
        if (result === '0' && char !== '.') {
          result = char
        } else {
          result += char
        }
      }
    }
    function calculate() {
      result = evaluate(result)
    }
</script>

<main>
  <div data-tauri-drag-region class="titlebar">
    <div class="titlebar-button" >
      <img
        src="https://api.iconify.design/mdi:window-minimize.svg"
        alt="minimize"
      />
    </div>
    <div class="titlebar-button" >
      <img
        src="https://api.iconify.design/mdi:window-maximize.svg"
        alt="maximize"
      />
    </div>
    <div class="titlebar-button" on:click={close}>
      <img src="https://api.iconify.design/mdi:close.svg" alt="close" />
    </div>
  </div>
  <div class="calc">
    <input id="out" bind:value={result} type="text">
    <div class="val" on:click={clear} >C</div>
    <div class="val" on:click={operator('/')} >/</div>
    <div class="val" on:click={operator('*')} >*</div>
    <div class="val" on:click={operator('-')} >-</div>
    <div class="val" on:click={operator('1')} >1</div>
    <div class="val" on:click={operator('2')} >2</div>
    <div class="val" on:click={operator('3')} >3</div>
    <div class="val" on:click={operator('+')} >+</div>
    <div class="val" on:click={operator('4')} >4</div>
    <div class="val" on:click={operator('5')} >5</div>
    <div class="val" on:click={operator('6')} >6</div>
    <div class="val equal" on:click={calculate} >=</div>
    <div class="val" on:click={operator('7')} >7</div>
    <div class="val" on:click={operator('8')} >8</div>
    <div class="val" on:click={operator('9')} >9</div>
    <div class="val zero" on:click={operator('0')} >0</div>
    <div class="val" on:click={operator('.')} >.</div>
  </div>
</main>

<style>
  .calc {
    text-align: center;
    padding-top: 0em;
    margin-top: 2em;
    display:grid;
    gap:0.5rem;
    grid-template-columns: repeat(4, minmax(20px, 1fr));
    grid-auto-rows: 2rem;
    grid-auto-columns: 3rem;
    align-content:center;
  }

  #out {
    grid-column: span 4 / auto;
    text-align:right;
    height: 2em
  }

  .val {
    background-color:grey;
    cursor:default;
    padding-top:5px
  }

  .val:hover {
    background-color:aqua;
  }

  .equal {
    grid-row: span 3 / auto;
  }

  .zero {
    grid-column: span 2 / auto;
  }

  .titlebar {
    height: 30px;
    background: #329ea3;
    user-select: none;
    display: flex;
    justify-content: flex-end;
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
  }
  .titlebar-button {
    display: inline-flex;
    justify-content: center;
    align-items: center;
    width: 30px;
    height: 30px;
  }
  .titlebar-button:hover {
    background: #5bbec3;
  }
</style>
