---
layout: post
title: "Data Visualization Tools"
date: 2018-12-12 22:00:00 +0100
category: tutorial
tagline: ""
tags: [Data Science, Data Visualization, Python, JavaScript, BI]
abstract : "Data visualization is an important part for data analysis including raw data exploration and results presentation. I will introduce some tools for data visualization."
---
{% include JB/setup %}

* [Introduction](#introduction)
* [Candela](#candela)
  * [Installation](#installation)
  * [Components](#components)
* [Datawrapper](#datawrapper)
* [Google Data Studio](#google-data-studio)
* [Google Charts](#google-charts)
* [Leaflet](#leaflet)
* [MyHeatMap](#myheatmap)
* [Palladio](#palladio)
* [RawGraphs](#rawgraphs)
* [Tableau](#tableau)
  * [Tableau Commercial](#tableau-commercial)
  * [Tableau Public](#tableau-public)
* [Timeline](#timeline)
* [Chartist.js](#chartist.js)
* [ColorBrewer](#colorbrewer)
* [D3.js](#d3js)
* [Plotly](#plotly)
* [Polymaps](#polymaps)
* [GanttPro](#ganttpro)
* [Qlik](#qlik)
  * [QlikView](#qlikview)
  * [Qlik Sense](#qlik-sense)
* [SAS Visual Analytics](#sas-visual-analytics)
* [Chart.js](#chart.js)
* [Summary](#summary)
* [References](#references)


## Introduction

Data visualization is to use tools to create statistical charts, plots, graphics or tables to present data visually.
The goal of data visualization is to present data to audience clearly and efficiently. It makes complex data easier to be accessible and understandable.

Data visualization is an important part for data analysis including raw data exploration and results presentation.

Common representation usages:

| Type of information | Type of chart |
|---|---|
| Components  | Pie chart |
| Item        | Bar chart |
| Time Series | Line chart |
| Frequency   | Line chart, Histogram |
| Correlation | Scatter plot, side-by-side bar chart |

Here are some tools for data visualization.

## Candela

[Candela](https://candela.readthedocs.io/en/latest/) is an open-source suite of inter-operable web visualization components.
It provides library for JavaScript, package for Python and R.

![candela]({{ site.url }}/assets/images/data_visualization/candela.png){:height="300px" width="600px"}

### Installation

For **JavaScript**,
```bash
npm install candela
```
Then the js file can be found at ```node_modules/candela/dist/candela[.min].js```.

For **Python**,
```bash
pip install pycandela
```

For **R**, to install directly from GitHub:
```R
install.packages('devtools')
devtools::install_github('Kitware/candela', subdir='R/candela', dependencies = TRUE)
```
to install from a Git checkout:
```R
setwd('/path/to/candela/R/candela')
install.packages('devtools')
devtools::install(dependencies = TRUE)
devtools::check()
```

### Components

Components list:

1. BarChart
2. BoxPlot
3. GanttChart
4. Geo
5. GeoDots
6. GLO (Graph-Level Operations)
7. Histogram
8. LineChart
9. LineUp
10. OnSet
11. ScatterPlot
12. ScatterPlotMatrix
13. SentenTree
14. SimilarityGraph
15. TreeHeatmap
16. UpSet


## Datawrapper

[Datawrapper](https://www.datawrapper.de/) is a on-line data visualization tool. Users can create charts, reports and maps on-line easily.
The free version allows a single user to create 10,000 chart views and 1 locator maps per month.
It also works on mobile, tablet and desktop devices.

![datawrapper]({{ site.url }}/assets/images/data_visualization/datawrapper.png){:width="600px"}

Charts and Maps:
1. Bar charts: normal bar chart, stacked bar chart, bullet bar chart, split bar chart, grouped bar chart, population pyramid.
2. Column charts: normal column chart, grouped column chart, stacked column chart.
3. Line charts: normal line chart, slope chart.
4. Area chart: normal, pie chart, donut chart.
5. Tables: short table, long table.
6. Scatter plots.
7. Dot charts: dot plot, range plot, arrow plot.
7. Maps: symbol map, choropleth map.
8. Locator maps.

## Google Data Studio

[Google Data Studio](https://marketingplatform.google.com/about/data-studio/) is also a web data visualization tool.
You only need a Google account to sign up and can connect it with other Google products such as Google Analytics and Google Sheets for data sources.

![google data studio]({{ site.url }}/assets/images/data_visualization/googledatastudio.png){:width="600px"}

Google Data Studio provides tools to easily create detailed reports including descriptions, tables and charts.

Charts and Maps:
1. Table
2. Scorecard
3. Time series
4. Bar
5. Pie
6. Goe map
7. Line
8. Area
9. Scatter
10. Pivot table
11. Bullet


## Google Charts

[Google Charts](https://developers.google.com/chart/) provides free and simple tools for interactive charts and data visualization.

The most common way to use Google Charts is with to embed simple JavaScript in web page. Load some Google Chart libraries, list the data to be charted, select options to customize chart, and finally create a chart object with an id. Then, later in the web page, create a <div> with that id to display the Google Chart.

![google charts]({{ site.url }}/assets/images/data_visualization/googlecharts.png){:width="600px"}

Charts:
1. Geo Chart
2. Scatter Chart
3. Column Chart
4. Histogram
5. Bar Chart
6. Combo Chart
7. Area Chart
8. Stepped Area Chart
9. Line Chart
10. Pie Chart
11. Bubble Chart
12. Donut Chart
13. Org Chart
14. Treemap
15. Table
16. Timeline
17. Gauge
18. Candlestick Chart


## Leaflet

[Leaflet](https://leafletjs.com/) is an open-source JavaScript library for mobile-friendly interactive maps.
It has lots of mapping features and can be extended with lots of plugins.

![Leaflet]({{ site.url }}/assets/images/data_visualization/leaflet.png){:width="600px"}


## MyHeatMap

[MyHeatMap](https://myheatmap.com/) is a free web tool to create interactive heat maps by uploading a CSV file with data. It is a simple tool to view geographic data interactively.

But the limitation is that, the free version only allows to create maps with 20 data points for each.

![MyHeatMap]({{ site.url }}/assets/images/data_visualization/myheatmap.png){:width="600px"}


## Palladio

[Palladio](http://hdlab.stanford.edu/palladio/) can visualize complex historical data with ease.
Its data visualization views include Map view, Graph view, Table view and Gallery view.
1. Upload data from spreadsheet, tabular(.csv, .tab, .tsv) or a public Dropbox file.
2. In Map view, coordinates data can be seen as points on a map. Relationships between distinct points can be connected by lines.
3. In Graph view, relationships can be visualized between any two dimensions of data. Information will be displayed as nodes connected by lines.
4. In Table(List) view, dimensions of data can be arranged to make customized lists.
5. In Gallery view, data can be displayed within a grid setting for quick reference.

![Palladio]({{ site.url }}/assets/images/data_visualization/palladio.png){:width="600px"}


## RawGraphs

[RawGraphs](https://rawgraphs.io/) is an open source web tool to create custom vector-based visualizations on top of d4.js library.
RawGraphs is also highly customizable and extensible, accepting new custom charts defined by users.

![RawGraphs]({{ site.url }}/assets/images/data_visualization/rawgraphs.png){:width="600px"}

The process:
1. Upload data with delimiter-separated values (i.e. csv and tsv files) or copied-and-pasted texts from other applications (e.g. Microsoft Excel, Google Spreadsheets, TextEdit).
2. Choose a chart from those visual models.
3. Customize visualization after mapping data dimensions.
4. Export visualizations as vector (SVG) or raster (PNG) images.

Charts:
1. Contour Plot.
2. Convex Hull.
3. Hexagonal Binning.
4. Scatter Plot.
5. Voronoi Tessellation.
6. Beeswarm Plot.
7. Box Plot.
8. Circular Dendrogram.
9. Cluster Dendrogram.
10. Circle Packing.
11. Sunburst.
12. Treemap.
13. Alluvial Diagram.
14. Parallel Coordinates.
15. Bar Chart.
16. Pie Chart.
17. Gantt Chart.
18. Area Graph.
19. Bump Chart.
20. Horizon Graph.
21. Streamgraph.


## Tableau

[Tableau](https://www.tableau.com/) is a famous business intelligence tool. It contains several products including Tableau Desktop, Tableau Prep, Tableau Online and Tableau Server. It is a powerful, secure, and flexible end-to-end analysis platform.

### Tableau Commercial

Tableau Prep is the tool to prepare the data for analysis.
It contains two products: Tableau Prep Builder for building data flows and Tableau Prep Conductor for sharing flows and managing. The builder is used mainly for combining, shaping and cleaning data.
The data source could be Amazon Aurora, Google Cloud SQL, IBM DB2, Microsoft products, MongoDB, MySQL, Oracle, PostgreSQL, SAP Sybase, Teradata, Text file.

Tableau Desktop is the main tool to build the analytics locally by connecting to varying data sources, dragging-and-dropping visually to create diagrams.
It could connect to more data sources: Amazon, Google, SAP, Dropbox, IBM DB2, JSON files, KML files, MariaDB, Microsoft products, Microsoft Azure, MongoDB, MySQL OData, Oracle, PostgreSQL, R files, SPSS files, Teradata, text files, Web data connector.

Tableau Online and server is used to share data and insights. User could try Tableau Online directly on the web.
Tableau Online could connect to cloud databases like Amazon Redshift and Google BigQuery and automatically refresh data.

The image below shows the an example on Tableau Online.

![Tableau Online]({{ site.url }}/assets/images/data_visualization/tableauonline.png){:width="600px"}

### Tableau Public

[Tableau Public](https://public.tableau.com/) is a free version of Tableau with 10 GB of storage. With it, users can also create and share interactive charts, graphs and maps.
The data source could be Excel, text files, Google Sheets, web data connectors, spatial files.
It is also quite powerful.

![Tableau Public]({{ site.url }}/assets/images/data_visualization/tableaupublic.png){:width="600px"}


## Timeline

[Timeline](https://timeline.knightlab.com/) is an open-source web tool to create visually rich, interactive timelines.
Use a Google Drive spreadsheet to create a timeline from the template. Use JSON skills to create custom installations.

![Timeline]({{ site.url }}/assets/images/data_visualization/timeline.png){:width="600px"}


## Chartist.js

[Chartist.js](https://gionkunz.github.io/chartist-js/) is a simple and lightweight library built with SVG to create responsive charts on website.

Chartist.js offers great flexibility and is customizable.
Specifying the style of chart in CSS is not only cleaner but also enables to use awesome CSS animations and transitions to be applied to SVG elements.
It has even added a simple but powerful animation API that allows to create SMIL animations in a more convenient way.

![Chartist.js]({{ site.url }}/assets/images/data_visualization/chartistjs.png){:width="600px"}

Chart types:
1. Line Chart.
2. Bar Chart.
3. Pie Chart.

## ColorBrewer

[ColorBrewer](http://colorbrewer2.org) is a free tool that can be used to make maps better in terms of color schemes. The tool makes it easy to differentiate colors on a complex map.

![ColorBrewer]({{ site.url }}/assets/images/data_visualization/colorbrewer.png){:width="600px"}

The version 1.0 is based on Flash. And the version 2.0 is based on JavaScript and CSS.


## D3.js

[D3.js](https://d3js.org/) (Data-Driven Documents) is an JavaScript libarry for visualizing data using web standards.
D3 allows to bind arbitrary data to a Document Object Model (DOM) with SVG, Canvas and HTML, and then apply data-driven transformations to the document.
D3 API contains several hundred functions.

![D3.js]({{ site.url }}/assets/images/data_visualization/d3js.png){:width="600px"}


## Plotly

[Plotly](https://plot.ly/) offers the fastest growing open-source visualization libraries for R, Python and JavaScript. Its products include Dash, Chart Studio and Plotly.js.

Dash is a Python framework for building analytical web applications without requirements of JavaScript. It is built on Plotly.js, React and Flask.
Dash is lightweight and provides a simple interface for UI controls.

Chart Studio is used to create and edit D3.js and WebGL charts online. Users can make D3 and WebGLcharts entirely without code by uploading a CSV file or connect to a SQL database through Falcon.

Plotly.js is a high-level, declarative charting library, built on top of d3.js and stack.gl. plotly.js ships with 20 chart types, including 3D charts, statistical graphs, and SVG maps. 

![Plotly](https://tamarack-prismic.imgix.net/plotly%2Fe5cbdc96-2ff0-493a-98a4-ddeba7a40b58_optimize-drug-discovery.gif){:width="600px"}


## Polymaps

[Polymaps](http://polymaps.org/) is a JavaScript library for image- and vector-tiled maps using SVG.
Polymaps provides speedy display of multi-zoom datasets over maps, and supports a variety of visual presentations for tiled vector data, in addition to the usual cartography from OpenStreetMap, CloudMade, Bing, and other providers of image-based web maps.

![Polymaps]({{ site.url }}/assets/images/data_visualization/polymaps.png){:width="600px"}


## Dygraphs

[Dygraphs](http://dygraphs.com/) is a fast, flexible open source JavaScript charting library. It allows to explore and interpret dense data sets.
This tool is highly customizable and offers strong support for error bars / confidence intervals.

![Dygraphs]({{ site.url }}/assets/images/data_visualization/dygraphs.png){:width="600px"}


## GanttPro

[GanttPro](https://ganttpro.com/) is a project management tool to create online gantt charts to plan project and manage tasks.

![GanttPro]({{ site.url }}/assets/images/data_visualization/ganttpro.gif){:width="600px"}

But it is not a free tool. Users can only get a 15-days trial.


## Qlik

[Qlik](https://www.qlik.com/) is a powerful BI tools platform. It provides several products:
1. Qlik Sense: a multi-cloud solution for modern BI.
2. Qlik Analytics Platform: used for embedded and custom analytics.
3. Qlik View: used to build and deploy interactive, guided analytics applications.
4. Qlik Core: a native cloud analytics development platform.
5. Qlik Data Catalyst: used to deliver analytics-ready data for enterprise.
6. Qlik GeoAnalytics: used for location-based analytics.

Among these tools, QlikView and Qlik Sense are the two main products. Qlik Softwares for enterprises are not free. But Qlik Sense cloud basic, Qlik Sense desktop version and QlikView personal edition are free for users to try.

### QlikView

[QlikView](https://www.qlik.com/us/products/qlikview) is for guided analytics.
It allows users to rapidly build and deploy analytic applications and is used for day-to-day tasks, analyzing data with a slightly configurable dashboard.

![QlikView]({{ site.url }}/assets/images/data_visualization/qlikview.png){:width="600px"}

### Qlik Sense

[Qlik Sense](https://www.qlik.com/us/products/qlik-sense) is for self-service, guided, embedded visualization and reporting.
It allows associating different data sources and fully configuring the visualizations, allowing to follow an individual discovery path through the data.

![Qlik Sense]({{ site.url }}/assets/images/data_visualization/qliksense.gif){:width="600px"}


## SAS Visual Analytics

[SAS Visual Analytics](https://www.sas.com/en_in/software/visual-analytics.html) is a BI tool for data exploration, data visualization and prediction with its highly visual, drag-and-drop data interface.

SAS Visual Analytics can be used for self-service data preparation, data visualizations, reporting, self-service analytics, text analysis and location analytics.

Analytical visualizations include:
- Box plots.
- Heat maps.
- Animated bubble charts.
- Network diagrams.
- Correlation matrices.
- Line charts with forecasting.
- Parallel coordinates plots.
- Donut charts.
- Decision trees.
- And more.

SAS Visual Analytics even offers Apps for mobile devices.

![SAS Visual Analytics]({{ site.url }}/assets/images/data_visualization/sasvisualanalytics.gif){:width="600px"}


## Chart.js

[Chart.js](https://www.chartjs.org/) is an open source JavaScript library to create simple, clean and engaging HTML5-based charts with several chart types and animation.
It also provides some APIs for developers to extend and enhance the library.

![Chart.js]({{ site.url }}/assets/images/data_visualization/chartjs.png){:width="600px"}

Chart types:
1. Bar charts: vertical, horizontal, stacked, stacked groups, multi axis.
2. Line charts: basic, multi axis, stepped, interpolation, line styles, point styles, point size.
3. Area charts: boundaries, datasets, stacked, radar.
4. Scatter.
5. Pie chart.
6. Bubble Chart


## Summary

Personally, I will recommend:
- Python: Candela, **Plotly**,
- JavaScript: Google Charts, **D3.js**.
- Others: Google Data Studio, Tableau, Qlik


## References

1. [20 Free and Open-Source Data Visualization Tools](https://dzone.com/articles/20-free-and-open-source-data-visualization-tools)
2. [Top 5 Data Visualization Tools for every Data Scientist](https://www.datasciencelearner.com/top-5-data-visualization-tools-data-scientist/)
3. [Candela](https://candela.readthedocs.io/en/latest/)
4. [Datawrapper](https://www.datawrapper.de/)
5. [Google Data Studio](https://marketingplatform.google.com/about/data-studio/)
6. [Google Charts](https://developers.google.com/chart/)
7. [Leaflet](https://leafletjs.com/)
8. [MyHeatMap](https://myheatmap.com/)
9. [Palladio](http://hdlab.stanford.edu/palladio/)
10. [RawGraphs](https://rawgraphs.io/)
11. [Tableau](https://www.tableau.com/)
12. [Tableau Public](https://public.tableau.com/)
13. [Timeline](https://timeline.knightlab.com/)
14. [Chartist.js](https://gionkunz.github.io/chartist-js/)
15. [ColorBrewer](http://colorbrewer2.org)
16. [D3.js](https://d3js.org/)
17. [Plotly](https://plot.ly/)
18. [Polymaps](http://polymaps.org/)
19. [Dygraphs](http://dygraphs.com/)
20. [GanttPro](https://ganttpro.com/)
21. [Qlik](https://www.qlik.com/)
22. [QlikView](https://www.qlik.com/us/products/qlikview)
23. [Qlik Sense](https://www.qlik.com/us/products/qlik-sense)
24. [SAS Visual Analytics](https://www.sas.com/en_in/software/visual-analytics.html)
25. [Chart.js](https://www.chartjs.org/)
