---
layout: post
title: "Your Post Title"
date: 2012-05-02 07:20
comments: true
categories: 
---

<!-- Make sure to include D3 first or else the IIFEs won't work. -->
<script src="http://d3js.org/d3.v2.js"></script> 

<!-- CSS Styles: -->
<div>
  <style type="text/css">

    .chart {
      font-family: Arial, sans-serif;
      font-size: 10px;
      margin-top: -40px;
    }

    .bar {
      fill: steelblue;
    }

    .axis path, .axis line {
      fill: none;
      stroke: #000;
      shape-rendering: crispEdges;
    }

  </style>
</div>

<!-- Global Variables and Handlers: -->
<script type="text/javascript">

  var data = [1, 1, 2, 3, 5, 8];

  var margin = {top: 40, right: 40, bottom: 40, left: 40},
      width = $('.entry-content').width(),
      height = 300;

  $(window).resize(function() {
    width = $('.entry-content').width();
  });

</script>

### Here's a Heading!
Here's an example D3 chart:

<!-- D3.js Chart -->
<div id='chart-1'></div>
<script type='text/javascript'>
(function() {

  function draw() {
    
    $('#chart-1').empty();

    var x = d3.scale.linear()
        .domain([0, d3.max(data)])
        .range([0, width - margin.left - margin.right]);

    var y = d3.scale.ordinal()
        .domain(d3.range(data.length))
        .rangeRoundBands([height - margin.top - margin.bottom, 0], 0.2);

    var xAxis = d3.svg.axis()
        .scale(x)
        .orient('bottom')
        .tickPadding(8);

    var yAxis = d3.svg.axis()
        .scale(y)
        .orient('left')
        .tickPadding(8)
        .tickSize(0);

    var svg = d3.select('#chart-1').append('svg')
        .attr('width', width)
        .attr('height', height)
        .attr('class', 'chart')
      .append('g')
        .attr('transform', 'translate(' + margin.left + ', ' + margin.top + ')');

    svg.selectAll('.chart')
        .data(data)
      .enter().append('rect')
        .attr('class', 'bar')
        .attr('y', function(d, i) { return y(i) })
        .attr('width', x)
        .attr('height', y.rangeBand());

    svg.append('g')
        .attr('class', 'x axis')
        .attr('transform', 'translate(0, ' + y.rangeExtent()[1] + ')')
        .call(xAxis);

    svg.append('g')
        .attr('class', 'y axis')
        .call(yAxis)
      .selectAll('text')
        .text(function(d) { return String.fromCharCode(d + 65); });
    
  }

  draw();

  $(window).resize(function() {
    draw();
  });

})();
</script>

### Here's another heading!
Here's some awesome copy regarding that sweet, sweet bar chart!

