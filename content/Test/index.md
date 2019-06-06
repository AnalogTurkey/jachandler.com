+++
title = "Test"
description = "Test."
date = 2019-06-05
hidden = true
+++

<script src="https://cdn.plot.ly/plotly-latest.min.js"></script>

<div id="thisDiv">
      <!-- Plotly chart will be drawn inside this DIV -->
</div>
  
<script>
	var trace1 = {
		type: 'bar',
		x: [1, 2, 3, 4],
		y: [5, 10, 2, 8],
		marker: {
			color: '#C8A2C8',
			line: {
				width: 2.5
			}
		}
	};

	var data = [ trace1 ];
	

	Plotly.newPlot('thisDiv', data, {responsive: true});
	
	window.onresize = function() {
  Plotly.Plots.resize(my_Div);
};

//document.getElementById("thisDiv").setAttribute("width","55%");
//document.getElementById("thisDiv").setAttribute("style","border:1px solid indigo");
//document.getElementById("thisDiv").style.padding = "11px";

</script>