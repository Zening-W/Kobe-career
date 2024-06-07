<script>
    import { select } from "d3-selection";
    import { scaleLinear } from "d3-scale";
    import { line } from "d3-shape";
    import { axisBottom, axisLeft } from "d3-axis";
    // import { csv } from "d3-fetch";
    import { onMount } from "svelte";
    import { kobe_shaq } from "../datasets";
  
    let metric = 'pts'; 
    const data = kobe_shaq

    console.log('KPOBE', kobe_shaq)
  
    function createGraph() {
      // csv("public/assets/data/kobe_data_with_shaq.csv").then(data => {
        console.log("Loaded Data:", data); 
  
        data.forEach(d => console.log("Shaq_present value:", d.Shaq_present));
  
        const svg = select("#newGraph");
        svg.selectAll("*").remove(); 
  
        const margin = { top: 20, right: 30, bottom: 40, left: 40 };
        const width = 800 - margin.left - margin.right;
        const height = 400 - margin.top - margin.bottom;
  
        const svgContainer = svg
          .attr("width", width + margin.left + margin.right)
          .attr("height", height + margin.top + margin.bottom)
          .append("g")
          .attr("transform", `translate(${margin.left},${margin.top})`);
  
        const ages = data.map(d => +d.age);
        const maxMetric = Math.max(...data.map(d => +d[metric]));
  
        const x = scaleLinear()
          .domain([Math.min(...ages), Math.max(...ages)])
          .range([0, width]);
        const y = scaleLinear()
          .domain([0, maxMetric])
          .range([height, 0]);
  
        const lineGenerator = line()
          .x(d => x(d.age))
          .y(d => y(d[metric]));
  
        // const shaqPresentData = data.filter(d => String(d.Shaq_present) === "True");
        // const shaqAbsentData = data.filter(d => String(d.Shaq_present) === "False");
        const shaqPresentData = data.filter(d => d.Shaq_present === true);
        const shaqAbsentData = data.filter(d => d.Shaq_present === false);
  
        console.log("Shaq Present Data:", shaqPresentData); // Check filtered data
        console.log("Shaq Absent Data:", shaqAbsentData); // Check filtered data
  
        svgContainer.append("g")
          .attr("transform", `translate(0,${height})`)
          .call(axisBottom(x));
  
        svgContainer.append("g")
          .call(axisLeft(y));
  
        svgContainer.append("path")
          .datum(shaqPresentData)
          .attr("fill", "none")
          .attr("stroke", "steelblue")
          .attr("stroke-width", 1.5)
          .attr("d", lineGenerator);
  
        svgContainer.append("path")
          .datum(shaqAbsentData)
          .attr("fill", "none")
          .attr("stroke", "orange")
          .attr("stroke-width", 1.5)
          .attr("d", lineGenerator);
  
        
      // Add legend
      svgContainer.append("text")
        .attr("x", -40)
        .attr("y", height - 300 )
        .attr("fill", "steelblue")
        .text("With Shaq");

      svgContainer.append("text")
        .attr("x", 300)
        .attr("y", height - 300)
        .attr("fill", "orange")
        .text("Without Shaq");
    // }).catch(error => console.error('Error loading data:', error));
    }
  
    // Function to update the graph based on selected metric
    function updateGraph(selectedMetric) {
      metric = selectedMetric;
      createGraph();
    }
  
    // Create the graph after component is mounted
    onMount(() => {
      createGraph();
    });
  </script>
  
  <section>
    <div class="additional-content">
      <p class="additional-text">
        After exploring the dynamic duo of Kobe and Shaq, it's essential to delve into the statistical impacts they had on the game. The following graph illustrates some key performance metrics.
      </p>
      <div class="button-container">
        <button on:click={() => updateGraph('pts')}>Points</button>
        <button on:click={() => updateGraph('reb')}>Rebounds</button>
        <button on:click={() => updateGraph('ast')}>Assists</button>
        <button on:click={() => updateGraph('net_rating')}>Net Rating</button>
        <button on:click={() => updateGraph('oreb_pct')}>Offensive Rebound %</button>
        <button on:click={() => updateGraph('dreb_pct')}>Defensive Rebound %</button>
        <button on:click={() => updateGraph('usg_pct')}>Usage %</button>
        <button on:click={() => updateGraph('ts_pct')}>True Shooting %</button>
        <button on:click={() => updateGraph('ast_pct')}>Assist %</button>
      </div>
      <div class="graph-container">
        <svg id="newGraph"></svg>
      </div>
      <div class="conclusion">
        {#if metric === 'pts'}
          <p class="conclusion-text">
            <strong>Points (pts):</strong> 
            <br/>
            <strong>With Shaq:</strong> Kobe's points per game increased steadily, peaking around age 25, indicating his growing role in the team's offense.
            <br/>
            <strong>Without Shaq:</strong> Kobe's points per game remained high, showing his continued dominance as a scorer even after Shaq's departure. But there is a small decrease near the end of his retirement.
          </p>
        {/if}
        {#if metric === 'reb'}
          <p class="conclusion-text">
            <strong>Rebounds (reb):</strong>
            <br/>
            <strong>With Shaq:</strong> Except for the first few years, Kobe's rebounding numbers were relatively stable, reflecting his consistent contribution to the team's overall rebounding efforts.
            <br/>
            <strong>Without Shaq:</strong> There was a noticeable increase in Kobe's rebounds, suggesting he took on more responsibilities in this area after Shaq left.
          </p>
        {/if}
        {#if metric === 'ast'}
          <p class="conclusion-text">
            <strong>Assists (ast):</strong>
            <br/>
            <strong>With Shaq:</strong> Kobe's assists increased over time, demonstrating his ability to facilitate plays and create opportunities for teammates.
            <br/>
            <strong>Without Shaq:</strong> His assist numbers were high, indicating his role as a primary playmaker in addition to being a scorer.
          </p>
        {/if}
        {#if metric === 'net_rating'}
          <p class="conclusion-text">
            <strong>Net Rating:</strong>
            <br/>
            <strong>With Shaq:</strong> The team's net rating while Kobe was on the floor was positive, showcasing the effectiveness of the Kobe-Shaq duo.
            <br/>
            <strong>Without Shaq:</strong> The net rating remained strong, highlighting Kobe's ability to lead the team and contribute to its success.
          </p>
        {/if}
        {#if metric === 'oreb_pct'}
          <p class="conclusion-text">
            <strong>Offensive Rebound Percentage (oreb_pct):</strong>
            <br/>
            <strong>With Shaq:</strong> Kobe's offensive rebound percentage was modest, reflecting his position and role on the team.
            <br/>
            <strong>Without Shaq:</strong> There was a slight decrease, indicating a shift in securing offensive rebounds.
          </p>
        {/if}
        {#if metric === 'dreb_pct'}
          <p class="conclusion-text">
            <strong>Defensive Rebound Percentage (dreb_pct):</strong>
            <br/>
            <strong>With Shaq:</strong> The defensive rebound percentage was stable, showing Kobe's consistent defensive presence.
            <br/>
            <strong>Without Shaq:</strong> There was an increase, suggesting Kobe took on a larger defensive role.
          </p>
        {/if}
        {#if metric === 'usg_pct'}
          <p class="conclusion-text">
            <strong>Usage Percentage (usg_pct):</strong>
            <br/>
            <strong>With Shaq:</strong> Kobe's usage percentage increased, reflecting his growing importance in the team's offensive schemes.
            <br/>
            <strong>Without Shaq:</strong> The usage percentage was very high, indicating Kobe was the primary option on offense.
          </p>
        {/if}
        {#if metric === 'ts_pct'}
          <p class="conclusion-text">
            <strong>True Shooting Percentage (ts_pct):</strong>
            <br/>
            <strong>With Shaq:</strong> Kobe's true shooting percentage was efficient, demonstrating his effective scoring ability.
            <br/>
            <strong>Without Shaq:</strong> The efficiency remained high, showcasing Kobe's skill in maintaining scoring efficiency despite increased defensive focus.
          </p>
        {/if}
        {#if metric === 'ast_pct'}
          <p class="conclusion-text">
            <strong>Assist Percentage (ast_pct):</strong>
            <br/>
            <strong>With Shaq:</strong> Kobe's assist percentage increased, highlighting his role in creating scoring opportunities for teammates.
            <br/>
            <strong>Without Shaq:</strong> The assist percentage remained high, indicating Kobe's dual role as a scorer and facilitator. But there is a small decrease near the end of his retirement.
          </p>
        {/if}
        <p class="conclusion-text">
          Kobe Bryant's performance metrics demonstrate his versatility and ability to adapt to different team dynamics. During his time with Shaquille O'Neal, Kobe grew as a scorer and playmaker, contributing significantly to the team's success. After Shaq's departure, Kobe took on even more responsibilities, excelling in scoring, playmaking, and rebounding. His ability to maintain high efficiency and effectiveness in various aspects of the game solidifies his legacy as one of the greatest players in NBA history. The data illustrates Kobe's impact on the court, both as a part of the dominant duo with Shaq and as the primary leader of the Lakers in subsequent years.
        </p>
      </div>
      
      
    </div>
  </section>
  
  <style>
    .additional-text {
      font-size: 18px;
      margin-bottom: 2rem;
      text-align: center;
      max-width: 900px;
      margin-left: auto;
      margin-right: auto;
    }
  
    .button-container {
      display: flex;
      justify-content: center;
      gap: 5px;
      margin-bottom: 2rem;
    }
  
    .button-container button {
      padding: 0.3rem 0.6rem;
      font-size: 14px;
      cursor: pointer;
    }
  
    .graph-container {
      width: 100%;
      display: flex;
      justify-content: center;
    }
  
    #newGraph {
      width: 800px;
      height: 400px;
    }
  
    .conclusion-text {
      font-size: 18px;
      margin-bottom: 2rem;
      text-align: left;
      max-width: 900px;
      margin-left: auto;
      margin-right: auto;
    }
  </style>
  