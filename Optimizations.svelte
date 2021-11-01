<script>
  export let changePage;
  export let changeClickTime;
  export let clickTime;
  export let changeDifficulty;
  export let difficulty;
  export let targetShown;
  export let changeTargetShown;
  // export let changechronological;
  // export let Chronological;

  let ct = clickTime;
  function setClickTime(index) {
    ct = index + 2;
    changeClickTime(index + 2);
  }

  let d = difficulty;
  function setDifficulty(v) {
    d = v;
    changeDifficulty(v);
  }

  let ts = targetShown;
  function setTargetShown(i) {
    ts = i + 1;
    changeTargetShown(i + 1);
  }
</script>

<style>
  * {
    box-sizing: border-box;
  }

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
    width: 50%;
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
    color: white;
  }

  .row {
    width: 100%;
    display: flex;
    padding: 35px;
    font-size: 25px;
    justify-content: space-between;
    font-size: 18px;
  }
</style>

<main>
  <div class="box">
  <div class="row">
    <div style="display: flex; align-items: center;">TIME FOR CLICKING TARGETS</div>
    <div style="display: flex; align-items: center;">
    {#each new Array(9).fill(0) as v,i}
      <div on:click={() => setClickTime(i)} style="margin: 5px; cursor: pointer; color: {ct - 2 === i ? "#00f9c9" : "white"};">{i + 2}s</div>
    {/each}
    </div>

  </div>
  <div class="row">
    <div style="display: flex; align-items: center;">TIME FOR EACH TARGET SHOWN</div>
    <div style="display: flex; align-items: center;">
    {#each new Array(5).fill(0) as v,i}
      <div on:click={() => setTargetShown(i)} style="margin: 5px; cursor: pointer; color: {ts - 1 === i ? "#00f9c9" : "white"};">{i + 1}s</div>
    {/each}
    </div>

  </div>
    <div class="row">
      <div style="display: flex; align-items: center;">SIZE OF TARGETS</div>
      <div style="display: flex; align-items: center;">
        <div on:click={() => setDifficulty("Easy")} style="margin: 5px; cursor: pointer; color: {difficulty === "Easy" ? "#00f9c9" : "white"};">Easy</div>
        <div on:click={() => setDifficulty("Normal")} style="margin: 5px; cursor: pointer; color: {difficulty === "Normal" ? "#00f9c9" : "white"};">Normal</div>
        <div on:click={() => setDifficulty("Hard")} style="margin: 5px; cursor: pointer; color: {difficulty === "Hard" ? "#00f9c9" : "white"};">Hard</div>        
      </div>
    </div>
  <!-- </div>
    <div class="row">
    <div class="w60">
      <div class="left">Chronological</div>
    </div>
    <div class="w20">
      <div class="right">Yes, No</div>
    </div>
    <div class="w20">
      <div class="right">
        <select bind:value={Chronological} on:blur{() => changechronological(Chronological)}>
          <option value={true}>Yes</option>
          <option value={false}>No</option>
        </select>
      </div>
    </div>
  </div> -->
  
  <div on:click={() => changePage(0)} class="row" style="cursor: pointer; justify-content: center; color: #00f9c9;">
    BACK TO MENU
  </div>
  
</div>
</main>