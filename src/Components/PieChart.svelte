<script>
    import { onMount } from 'svelte';
    import * as d3 from 'd3';
    import { lakers1999, lakers2000, lakers2001, lakers2008, lakers2009 } from '../datasets';  // Adjust the import path as necessary
  
    let selectedYear = "1999";
    const years = ["1999", "2000", "2001", "2008", "2009"];
    const dataSets = {
      "1999": lakers1999,
      "2000": lakers2000,
      "2001": lakers2001,
      "2008": lakers2008,
      "2009": lakers2009,
    };
  
    onMount(() => {
      updateChart(selectedYear);
    });
  
    function updateChart(year) {
      const data = dataSets[year].map(d => ({ player: d.player_name, score: +d.pts }));
      d3.select("#chart").html(""); // Clear previous SVG
  
      const svg = d3.select("#chart").append("svg")
        .attr("width", 450)
        .attr("height", 450)
        .append("g")
        .attr("transform", "translate(225, 225)");
  
      const pie = d3.pie().value(d => d.score);
      const arc = d3.arc().innerRadius(0).outerRadius(180);
      const color = d3.scaleOrdinal(d3.schemeCategory10);
  
      svg.selectAll('path')
        .data(pie(data))
        .enter()
        .append('path')
        .attr('d', arc)
        .attr('fill', (d, i) => color(i))
        .attr("stroke", "white")
        .style("stroke-width", "2px")
        .style("opacity", 0.7)
        .on('mouseover', (event, d) => {
          let x = event.layerX; // Fixed tooltip placement
          let y = event.layerY;
          d3.select("#chart").append("text")
            .attr('id', 'tooltip')
            .attr('x', x)
            .attr('y', y - 10)
            .attr("text-anchor", "middle")
            .text(`${d.data.player}: ${d.data.score} points`);
        })
        .on('mouseout', () => {
          d3.select("#tooltip").remove();
        });
    }
  
    function handleButtonClick(year) {
      selectedYear = year;
      updateChart(year);
    }
  </script>
  
  <style>
    #chart-container {
      display: flex;
      flex-direction: column;
      align-items: center;
      text-align: center;
    }
  
    #chart {
      display: flex;
      justify-content: center;
      width: 100%;
      max-width: 600px;
      margin-top: 20px;
    }
  
    .button {
      margin: 5px;
      padding: 10px 20px;
      border: 1px solid transparent;
      background-color: #FDB927; 
      color: #552583;
      border-radius: 5px;
      cursor: pointer;
      font-size: 16px;
      transition: background-color 0.3s, transform 0.2s;
    }
  
    .button:hover, .button:focus {
      background-color: #08a9e9; /* Light blue on hover */
      transform: scale(1.05);
      outline: none;
    }
  
    .conclusion-text {
      font-size: 18px;
      margin-top: 20px;
      text-align: center;
      max-width: 900px;
      color: #FFFFFF; /* Optional: Set text color to white for better contrast */
    }
  </style>
  
  <div id="chart-container">
    <div>
      {#each years as year}
        <button class="button" on:click={() => handleButtonClick(year)}>{year}</button>
      {/each}
    </div>
    <div id="chart"></div>
    <div class="conclusion-text">
      In fact, from the first 2 years of data, Kobe and Shaq score the most to the championship, showing their great values and cooperation, while Shaq score even higher as he organizes attacks and serve as the tactical core of the team. In 2008 and 2009, however, Kobe took Shaq's role as a leader instead of purely being as a shooting guard, and Paul and Andrew took Kobe's past roles. Anyway, he still made great achievement without Shaq and transformed successfully in his later career.
    </div>
  </div>
  