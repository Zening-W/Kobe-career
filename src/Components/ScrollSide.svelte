<script>
  import Scrolly from "./Scrolly.svelte";
  import katexify from "../katexify";
  import { select, selectAll } from "d3-selection";

  // scroll iterator
  let value;

  // Paragraph text for scrolly
  $: steps = [
    `<h1 class='step-title'>Kobe and Shaq: The Dominant Duo</h1>
      <p>
        Kobe, with his unparalleled work ethic, scoring prowess, and clutch performances, complemented Shaq's sheer dominance in the paint, rebounding, and defensive presence. Their on-court synergy was evident as they executed seamless plays, from alley-oops to pick-and-rolls, overwhelming their opponents with a blend of finesse and power. This partnership not only brought championships to Los Angeles but also captivated fans worldwide, leaving an indelible mark on the league.
      </p>`,
    `<h1 class='step-title'>Their Tumultuous Relationship</h1>
      <p>
        Despite their success, the relationship between Kobe and Shaq was often tumultuous, marked by contrasting personalities and occasional public feuds. Shaq's laid-back demeanor and Kobe's intense, laser-focused approach to the game sometimes clashed, leading to tensions that were well-documented in the media. However, these challenges did not diminish their individual and collective brilliance on the court. After Shaq's departure to the Miami Heat in 2004, both players continued to achieve great success independently, with Kobe leading the Lakers to two more championships and Shaq winning another title with the Heat. Over time, their mutual respect and appreciation for each other's contributions grew, solidifying their legacy as one of the greatest duos in basketball history.
      </p>`
  ];

  const target2event = {
    0: () => {
      // Your event for step 0
    },
    1: () => {
      select("#chart1").style("background-color", "red");
      select("#chart2").style("background-color", "green");
    },
    2: () => {
      select("#chart1").style("background-color", "purple");
      select("#chart2").style("background-color", "coral");
    },
  };

  $: if (typeof value !== "undefined") target2event[value]();
</script>

<h2 class="body-header">Kobe and Shaq</h2>
<p class="body-text white-text">
  Kobe Bryant and Shaquille O'Neal formed one of the most dominant duos in NBA history during their time with the Los Angeles Lakers. Together, they led the Lakers to three consecutive NBA championships from 2000 to 2002, creating a dynasty that was defined by their unique combination of skill and physicality.
</p>
<section>
  <!-- scroll container -->
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
        <svg id="chart1"></svg>
      </div>
      <div class="chart-two">
        <svg id="chart2"></svg>
      </div>
    </div>
  </div>
  <br /><br />
  <p class="body-text"></p>
</section>

<style>
  #chart1,
  #chart2 {
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
  /* space after scroll is finished */
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
    font-family: var(--font-main);
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

  /* make side centered */
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

  .white-text {
    color: white;
  }

  .body-header {
  color: white;
}
</style>