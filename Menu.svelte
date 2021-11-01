<script>
  export let changePage;
</script>

<style>
  :root {
    --gray: #232833;
    --black: #1d212c;
    --green: #00f9c9;
  }

  .box {
    background-color: var(--black);
    border: 3px solid var(--green);
    border-radius: 20px;
    box-shadow: 0px 0px 10px 0px var(--green);
    width: 500px;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 50px;
  }

  main {
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  }
  .Menu {
    margin: 100px 40px 40px 40px;
    font-size: 40px;
    color: var(--green);
  }
  .borderMenu {
    font-size: 30px;
    color: white;
    margin: 10px;
  }
</style>

<main>
  <div class="box">
  <div class="Menu">AIM-TRAINER</div>
  <div style="cursor: pointer;" class="borderMenu" on:click={() => changePage(2)}>START</div>
  <div style="cursor: pointer;" class="borderMenu" on:click={() => changePage(1)}>OPTIMIZATIONS</div>
  </div>
</main>