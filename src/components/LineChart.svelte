<script>
  import * as d3 from "d3";
  import { onMount } from "svelte";

  export let data;

  function drawChart(dataset) {
    const yAccessor = (d) => d.price;
    const xAccessor = (d) => d.date;

    const dimensions = {
      width: window.innerWidth * 0.9,
      height: 400,
      margin: {
        top: 15,
        right: 15,
        bottom: 40,
        left: 60,
      },
    };

    dimensions.boundedWidth =
      dimensions.width - dimensions.margin.left - dimensions.margin.right;

    dimensions.boundedHeight =
      dimensions.height - dimensions.margin.top - dimensions.margin.bottom;

    // Wrapper
    const wrapper = d3
      .select("#wrapper")
      .append("svg")
      .attr("width", dimensions.width)
      .attr("height", dimensions.height);

    // Gradient
    const defs = d3.select("svg").append("defs");
    const gradient = defs.append("linearGradient").attr("id", "svgGradient");

    gradient
      .append("stop")
      .attr("class", "start")
      .attr("offset", "0%")
      .attr("stop-color", "white")
      .attr("stop-opacity", 1);

    gradient
      .append("stop")
      .attr("class", "end")
      .attr("offset", "100%")
      .attr("stop-color", "white")
      .attr("stop-opacity", 0);

    // Bounds
    const bounds = wrapper
      .append("g")
      .style(
        "transform",
        `translate(${dimensions.margin.left}px, ${dimensions.margin.top}px)`
      );

    // Scales
    const yScale = d3
      .scaleLinear()
      .domain(d3.extent(dataset, yAccessor))
      .range([dimensions.boundedHeight, 0])
      .nice();

    const xScale = d3
      .scaleTime()
      .domain(d3.extent(dataset, xAccessor))
      .range([0, dimensions.boundedWidth]);

    // Area Generator
    const areaGenerator = d3
      .area()
      .x((d) => xScale(xAccessor(d)))
      .y0(dimensions.boundedHeight)
      .y1((d) => yScale(yAccessor(d)));

    const area = bounds
      .append("path")
      .attr("d", areaGenerator(dataset))
      .attr("fill", "#eeecfa");

    // Line Generator
    const lineGenerator = d3
      .line()
      .x((d) => xScale(xAccessor(d)))
      .y((d) => yScale(yAccessor(d)));

    const line = bounds
      .append("path")
      .attr("d", lineGenerator(dataset))
      .attr("fill", "none")
      .attr("stroke", "#695eb6")
      .attr("stroke-width", 1);

    // Max line and circle
    const xPoint = xScale(xAccessor(dataset[dataset.length - 1]));
    const yPoint = yScale(yAccessor(dataset[dataset.length - 1]));

    // Price level line
    const priceLine = bounds
      .append("line")
      .style("stroke", "hsl(248, 38%, 54%, 0.4)")
      .style("stroke-width", 1)
      .attr("x1", 0)
      .attr("y1", yScale(yAccessor(dataset[dataset.length - 1])))
      .attr("x2", xScale(xAccessor(dataset[dataset.length - 1])))
      .attr("y2", yScale(yAccessor(dataset[dataset.length - 1])));

    const circleOutline = bounds
      .append("circle")
      .style("fill", "#eeecfa")
      .style("stroke", "hsla(195, 100%, 50%, 0.4)")
      .style("stroke-width", 5)
      .attr("cx", xPoint)
      .attr("cy", yPoint)
      .attr("r", 4);

    const circleMain = bounds
      .append("circle")
      .style("fill", "#eeecfa")
      .style("stroke", "#695eb6")
      .attr("cx", xPoint)
      .attr("cy", yPoint)
      .attr("r", 3);

    // Gradient Rect
    const rect = bounds
      .append("rect")
      .style("fill", "url(#svgGradient)")
      .attr("x", 0)
      .attr("y", 0)
      .attr("width", 50)
      .attr("height", dimensions.boundedHeight);

    // Axes
    const yAxisGenerator = d3.axisLeft().scale(yScale).ticks(5);

    const yAxis = bounds
      .append("g")
      .attr("class", "yaxis")
      .call(yAxisGenerator);

    const xAxisGenerator = d3.axisBottom().scale(xScale).ticks(4);

    const xAxis = bounds
      .append("g")
      .call(xAxisGenerator)
      .style("transform", `translateY(${dimensions.boundedHeight}px)`);
  }

  onMount(() => {
    drawChart(data);
  });
</script>

<div id="wrapper" />

<style>
  div {
    text-align: center;
  }
</style>
