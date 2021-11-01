<script>
  import Menu from "./Menu.svelte";
  import Optimizations from "./Optimizations.svelte";
  import Game from "./Game.svelte";
  import Death from "/Death.svelte";
  let page = 0;

  let clickTime = 2;
  function changeClickTime(value) {
    clickTime = value;
  }

  let difficulty = "Normal";
  function changeDifficulty(value) {
    difficulty = value;
  }
  let targetShown = 2;
  function changeTargetShown(value) {
    targetShown = value;
  }
  // let Chronological = true;
  // function changechronological(valie) {
  //   Chronological = value;
  // }

  function changePage(num) {
    page = num;
  }
</script>

<main>
  <div class="header"></div>
  {#if page === 0}
    <Menu changePage={changePage}/>
  {:else if page === 1}
    <Optimizations changePage={changePage} difficulty={difficulty} changeDifficulty={changeDifficulty} changeClickTime={changeClickTime} clickTime={clickTime} targetShown={targetShown} changeTargetShown={changeTargetShown}/>
 <!-- changechronological={changechronological} -->
  {:else if page === 2}

    <Game changePage={changePage} difficulty={difficulty} clicktime={clickTime} targetshown={targetShown} />
   {:else}

    <Death changePage={changePage}/>
  {/if}
</main>

<style>
  :root {
    --gray: #232833;
    --black: #1d212c;
    --green: #00f9c9;
  }

  main {
    height: 100%;
    background-color: var(--gray);
  }
</style>