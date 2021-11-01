<script>
  export let changePage;
  export let difficulty;
  export let targetshown;
  export let clicktime;

  let score = 0;
  let lives = 3;
  let hits = 0;
  let level = 1;

  let ct = parseInt(clicktime);
  let ts = parseInt(targetshown);

  // Easy 200
  // Medium 150
  // Hard 100

  function setSize() {
    if (difficulty === "Easy") {
      return 100;
    } else if (difficulty === "Normal") {
      return 80;
    } else {
      return 50;
    }
  }

  function setBorder() {
    if (difficulty === "Easy") {
      return 9;
    } else if (difficulty === "Normal") {
      return 7;
    } else {
      return 2;
    }
  }

  let x = 47.5;
  let y = 47.5;

  let playing = false;
  function start() {
    playing = true;
    level = 1;
    lives = 3;
    hits = 0;
    score = 0;
  }

  function randomSpot() {
    x = Math.floor(Math.random() * 60) + 20;
    y = Math.floor(Math.random() * 30) + 20;

    startTimer();
    clickTimer();
  }

  function hitTarget() {
    if (!playing) start();
    score++;
    hits++;
    if (hits % 10 == 0) {
      level++;
    }
    randomSpot();
  }

  let targetTimer;
  let show = true;
  function startTimer() {
    show = true;
    clearInterval(targetTimer);
    targetTimer = setInterval(() => {
      show = false;
      clearInterval(targetTimer);
    }, ts * 1000 * ((110 - 10 * level) / 100));
  }

  let clickTime;
  let t = ct * 1000 * ((110 - 10 * level) / 100);
  let p = 100;
  function clickTimer() {
    t = ct * 1000 * ((110 - 10 * level) / 100);
    clearInterval(clickTime);
    clickTime = setInterval(() => {
      t -= 10;
      p = Math.floor((t / (ct * 1000 * ((110 - 10 * level) / 100))) * 100);
      if (t <= 0) {
        score--;
        lives--;
        if (lives < 0) {
          lives = 0;
        }
        if (lives === 0) {
          gameOver();
        } else {
          randomSpot();
        }
        clearInterval(clickTime);
      }
    }, 10);
  }

  let timer;
  function gameOver() {
    playing = false;
    show = true;
    clearInterval(clickTime);
    clearInterval(targetTimer);
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

  .f-green {
    color: var(--green);
  }

  main {
    height: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    background-image: url("bg_transparent.png.jpg");
    background-size: cover;
    background-position: center;
  }

  .top {
    height: 100px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 100%;
    background-color: var(--black);
    border-bottom: 1px solid var(--green);
    box-shadow: 0px 0px 5px 0px var(--green);
    color: white;
  }

  .top-field {
    margin: 30px;
    width: 20%;
    text-align: center;
  }
  .back {
    width: 20%;
    text-align: center;
    font-size: 20px;
    color: var(--green);
    cursor: pointer;
  }

  .game {
    height: 70%;
    width: 100%;
  }
  .target-outer {
    transition-duration: 0.1s;
    position: absolute;
    border-radius: 50%;
    padding: 10px;
    box-shadow: 0px 0px 5px 0px #00f9c9;
    cursor: pointer;
  }
  .target-middle {
    height: 100%;
    width: 100%;
    border-radius: 50%;
    padding: 10px;
    box-shadow: 0px 0px 5px 0px #00f9c9;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .target-inner {
    height: 100%;
    width: 100%;
    border-radius: 50%;
    background-color: #00f9c9;
    box-shadow: 0px 0px 5px 1px #00f9c9;
  }

  .health {
    height: 75px;
    background-color: var(--black);
    width: 75%;
    border-radius: 37.5px;
    border: 3px solid var(--green);
    box-shadow: 0px 0px 5px 0px #00f9c9;
    margin-bottom: 20px;
  }
  .box {
    height: 100%;
    background-color: var(--green);
    border-radius: 37.5px;
    box-shadow: 0px 0px 5px 0px #00f9c9;
  }
</style>

<main>
    <div class="top">
      <div class="back" on:click={() => changePage(0)}>Menu</div>
      <div class="top-field">LEVEL <span class="f-green">{level}</span></div>
      <div class = "top-field">SCORE <span class="f-green">{score}</span></div>
      <div class = "top-field">LIVES <span class="f-green">{lives}</span></div>
      <div class = "top-field">TARGETS HIT <span class="f-green">{hits}</span></div>      
      <div class="back"></div>
    </div>
    <div class="game">
      <div on:click={() => hitTarget()} class="target-outer" style="opacity: {show ? 1 : 0}; left: {x}%; bottom: {y}%; height: {setSize()}px; width: {setSize()}px; border: {setBorder()}px solid #00f9c9;">
        <div class="target-middle" style="border: {setBorder()}px solid #00f9c9;">
          <div class="target-inner"></div>
        </div>
      </div>
    </div>
    <div style="flex-grow: 1;"/>
    {#if !playing}
      <div style="font-size: 24px; color: white; transform: translateY(-100px);">Click the target to start!</div>
    {/if}
    <div class = "health">
      <div class ="box" style="width: {p}%;"></div>
    </div>
</main>
   