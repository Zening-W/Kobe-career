<script>
  import Scrolly from "./Scrolly.svelte";
  import katexify from "../katexify";
  import { scaleOrdinal } from "d3-scale";
  import { select, selectAll } from "d3-selection";

  const xKey = "weight";
  const yKey = "weight";
  const zKey = "outcome";
  const titleKey = "gender";

  const r = 10;

  const seriesNames = new Set();
  const seriesColors = ["#7e93ee", "#ff99ff"];

  let value;

  $: steps = [
    `<h1 class='step-title' style="font-family: 'Bebas Neue', sans-serif; font-size: 2rem; margin-bottom: 1rem;">Kobe Bryant's Career Highlights</h1>
    <p style="font-family: 'Bebas Neue', sans-serif; font-size: 1.5rem; line-height: 1.4;">
      Known as one of the greatest players in NBA history, Kobe's 20-year career with the Los Angeles Lakers was highlighted by five NBA championships, two Finals MVP awards, and 18 All-Star selections. His relentless work ethic, often referred to as the "Mamba Mentality," inspired not only his teammates but also countless athletes around the world to strive for excellence. Kobe's scoring ability, exemplified by his 81-point game in 2006, showcased his talent and determination, solidifying his place among the basketball elite.
    </p>`,
    `<h1 class='step-title' style="font-family: 'Bebas Neue', sans-serif; font-size: 2rem; margin-bottom: 1rem;">Kobe Bryant's Legacy</h1>
    <p style="font-family: 'Bebas Neue', sans-serif; font-size: 1.5rem; line-height: 1.4;">
      Beyond his achievements on the court, Kobe Bryant's impact extended into various aspects of popular culture and community service. He was a passionate advocate for youth sports, founding the Mamba Sports Academy to provide young athletes with training opportunities. Kobe also won an Academy Award for his animated short film "Dear Basketball," demonstrating his versatility and creative talent. His tragic death in 2020 left a profound void, but his legacy continues to inspire future generations to pursue their dreams with dedication and resilience.
    </p>`,
  ];

  const target2event = {
    0: () => {
      select("#chart3").style("background-color", "darkorange");
      select("#chart4").style("background-color", "black");
    },
    1: () => {
      select("#chart3").style("background-color", "salmon");
      select("#chart4").style("background-color", "pink");
    },
  };

  $: if (typeof value !== "undefined") target2event[value]();
</script>

<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&display=swap" rel="stylesheet">

<h2 class="body-header">Retirement and Legacy</h2>
<p class="body-text">
  Though passing away, Kobe Bryant's legacy transcends basketball, marked by his unparalleled dedication, skill, and influence both on and off the court.
</p>
<section>
  <div class="section-container">
    <div class="steps-container">
      <Scrolly bind:value>
        {#each steps as text, i}
          <div class="step" class:active={value === i}>
            <div class="step-content">{@html text}</div>
          </div>
        {/each}
        <div class="spacer" />
      </Scrolly>
    </div>
    <div class="charts-container">
      <div class="chart-one">
        <svg id="chart3" />
      </div>
      <div class="chart-two">
        <svg id="chart4" />
      </div>
    </div>
  </div>
  <br /><br />
  <p class="body-text"></p>
</section>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Bebas+Neue&display=swap');

  #chart3,
  #chart4 {
    width: 100%;
    height: 100%;
  }
  .chart-one {
    width: 100%;
    height: 100%;
    border: 3px solid skyblue;
  }
  .chart-two {
    width: 100%;
    height: 100%;
    border: 3px solid coral;
  }
  .spacer {
    height: 40vh;
  }
  .charts-container {
    position: sticky;
    top: 10%;
    display: grid;
    width: 50%;
    grid-template-columns: 100%;
    grid-row-gap: 2rem;
    grid-column-gap: 0rem;
    grid-template-rows: repeat(2, 1fr);
    height: 85vh;
    border: 3px solid black;
  }
  .section-container {
    margin-top: 1em;
    text-align: center;
    transition: background 100ms;
    display: flex;
  }
  .step {
    height: 110vh;
    display: flex;
    place-items: center;
    justify-content: center;
  }
  .step-content {
    font-size: 18px;
    background: var(--bg);
    color: #ccc;
    border-radius: 1px;
    padding: 0.5rem 1rem;
    display: flex;
    flex-direction: column;
    justify-content: center;
    transition: background 500ms ease;
    text-align: left;
    width: 75%;
    margin: auto;
    max-width: 500px;
    font-family: 'Bebas Neue', sans-serif;
    line-height: 1.3;
    border: 5px solid var(--default);
  }
  .step.active .step-content {
    background: #f1f3f3ee;
    color: var(--squid-ink);
  }
  .steps-container {
    height: 100%;
  }
  .steps-container {
    flex: 1 1 40%;
    z-index: 10;
  }
  .section-container {
    flex-direction: column-reverse;
  }
  .steps-container {
    pointer-events: none;
  }
  .charts-container {
    top: 7.5%;
    width: 75%;
    margin: auto;
  }
  .step {
    height: 130vh;
  }
  .step-content {
    width: 65%;
    max-width: 768px;
    font-size: 17px;
    line-height: 1.6;
  }
  .spacer {
    height: 100vh;
  }
  .body-header {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 2rem;
    margin-bottom: 1rem;
  }
  .body-text {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 1.5rem;
    line-height: 1.4;
  }
</style>


