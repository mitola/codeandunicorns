---
id: 1335
title: Graph play
date: 2015-08-30T21:55:34+00:00
author: Joao Pereira
layout: post
guid: https://codeandunicorns.com/?p=1335
permalink: /graph-play/
slide_template:
  - default
pyre_full_width:
  - 'no'
pyre_transparent_header:
  - default
avada_post_views_count:
  - "3578"
fusion_builder_status:
  - inactive
fusion_builder_content_backup:
  - |
    Using tables to store data in a database is so common many developers often apply the same relational-database-voodoo solutions and focus on code architecture instead. It's a convenient trap one might fall into when deadlines are tough or little attention is given to the type of information being stored. It's amazing how little graphs are considered as a solution to represent data, often perceived as too complex to translate into code.
    
    Ultimately the persistence of graph data translates into a table but the way you handle your data is completely different.
    
    The application of graphs in programming is <strong>huge</strong>, more than the typical minimum distance problems!
    <h3>Basics</h3>
    It is well worth to explore the <a href="https://en.wikipedia.org/wiki/Graph_(mathematics)">mathematical definitions</a> but I won't be covering so deeply every concept. Instead I will present a few simple examples that illustrate how much you can do with so little.
    
    First of all it's important to understand what I mean by node graph:
    
    [caption id="attachment_1358" align="alignnone" width="464"]<a href="https://codeandunicorns.com/wp-content/uploads/2015/08/undirected.png"><img class="size-full wp-image-1358" src="https://codeandunicorns.com/wp-content/uploads/2015/08/undirected.png" alt="Undirected 3 node graph" width="464" height="245" /></a> Undirected 3 node graph[/caption]
    
    Notice the example above is an <strong>undirected graph</strong>, this means it's possible to traverse the graph starting on <strong>A</strong> all the way to <strong>B</strong> and vice-versa. This wouldn't be the case if we had a <strong>directed graph</strong> instead:
    
    [caption id="attachment_1356" align="alignnone" width="464"]<a href="https://codeandunicorns.com/wp-content/uploads/2015/08/directed.png"><img class="size-full wp-image-1356" src="https://codeandunicorns.com/wp-content/uploads/2015/08/directed.png" alt="Directed 3 node graph" width="464" height="245" /></a> Directed 3 node graph[/caption]
    
    In this case we have the same graph but once we go from <strong>A</strong> to <strong>B</strong> we can't go back! Practically this can be translated to:
    
    [code language="js"]
    graph -&gt; getEdge('A','B'); //true
    graph -&gt; getEdge('B','A'); //undefined
    [/code]
    
    With <strong>direction</strong> we can define <strong>path constraints</strong>!
    <h4>Distance</h4>
    Say you'd like to add a value by going through an edge, in that case you are adding a <strong>distance</strong> or simply a <strong>label</strong>. With labels you can describe an <strong>operation</strong>:
    
    [caption id="attachment_1363" align="alignnone" width="464"]<a href="https://codeandunicorns.com/wp-content/uploads/2015/08/label.png"><img class="size-full wp-image-1363" src="https://codeandunicorns.com/wp-content/uploads/2015/08/label.png" alt="Undirected labeled graph" width="464" height="245" /></a> Undirected labeled graph[/caption]
    
    [code language="js"]
    graph -&gt; getEdge('A','B'); //+
    graph -&gt; getEdge('B','A'); //+
    graph -&gt; getEdge('B','C'); //-
    graph -&gt; getEdge('C','B'); //-
    [/code]
    
    ...similarly with distance values you can add <strong>rates</strong>:
    
    [caption id="attachment_1364" align="alignnone" width="464"]<a href="https://codeandunicorns.com/wp-content/uploads/2015/08/rate.jpg"><img class="size-full wp-image-1364" src="https://codeandunicorns.com/wp-content/uploads/2015/08/rate.jpg" alt="Undirected weighted graph" width="464" height="245" /></a> Undirected weighted graph[/caption]
    
    [code language="js"]
    graph -&gt; getEdge('A','B'); //0.5
    graph -&gt; getEdge('B','A'); //0.5
    graph -&gt; getEdge('B','C'); //1.2
    graph -&gt; getEdge('C','B'); //1.2
    [/code]
    
    <h4>Multigraphs</h4>
    Multigraphs offer a more broad range of solutions for complex graphs. We simply allow nodes to have more than one edge connecting the same nodes, how? You add a name to the edge of course.
    
    [caption id="attachment_1368" align="alignnone" width="455"]<a href="https://codeandunicorns.com/wp-content/uploads/2015/08/multi.jpg"><img class="size-full wp-image-1368" src="https://codeandunicorns.com/wp-content/uploads/2015/08/multi.jpg" alt="Undirected 3 node multigraph" width="455" height="323" /></a> Undirected 3 node multigraph[/caption]
    
    [code language="js"]
    graph -&gt; getEdge('A','B', 'input'); //ioread
    graph -&gt; getEdge('A','B', 'output'); //iowrite
    graph -&gt; getEdge('B','C', 'input'); //fileread
    graph -&gt; getEdge('B','C', 'output'); //filewrite
    [/code]
    
    This example is merely illustrative, my point being: if you're not used to graph theory I hope by now you start understanding the potential of what you can do if you own a good <strong>graph library</strong>.
    
    It's amazing the amount of times I've seen business logic <strong>hammered</strong> programatically. With graphs you can <strong>hide complexity</strong> and apply clear <strong>business logic</strong> loaded from a database (for example) promoting cleaner code instead of applying long, nested <strong>if</strong> blocks or unending configuration files.
    <h3>Concrete example</h3>
    Before yawns are had I'll play a bit with an example and for the sake of it I'll use javascript with the cool public <a href="https://github.com/cpettitt/graphlib">graphlib</a>.
    
    Say we have a worldwide online shop with multiple outposts (1 per continent) and we want to access shipping costs of a package. Before shipping to the customers' address the package has to first be shipped along to the nearest outpost. The scenario would look something like this:
    
    [caption id="attachment_1378" align="alignnone" width="633"]<a href="https://codeandunicorns.com/wp-content/uploads/2015/08/Untitled.jpg"><img class="size-full wp-image-1378" src="https://codeandunicorns.com/wp-content/uploads/2015/08/Untitled.jpg" alt="NA - North America SA - South America CE - Central Europe AF - Africa AS - Asia AU - Australia " width="633" height="404" /></a> NA - North America<br />SA - South America<br />CE - Central Europe<br />AF - Africa<br />AS - Asia<br />AU - Australia[/caption]
    
    Let also add some prices per trip:
    
    [table]
    From, To, Value
    CE,NA,14.85 $
    CE,SA,13.15 $
    CE,AF,6.20 $
    CE,AS,23.60 $
    SA,AF,13.15 $
    AS,AU,9.65 $
    [/table]
    
    ... this would be a bit boring so lets add a special constraint to spice it up. Our outpost in Africa managed to negotiate a great discount, valid only when shipping to North America. The shipping path stays the same but now we have a price exception.
    
    [table]
    From, To, Value
    AF,NA,13.15 $
    [/table]
    
    The problem with the exception is that if we wanted to retrieve the shortest path <strong>and</strong> the lowest cost possible it wouldn't work with one graph alone, i.e. if we imported both tables onto our graph via <strong>setEdge()</strong> every time we computed the shortest path between Africa and North America the result would be a direct connection between Africa and North America thus violating our first constraints.
    
    No biggie we can solve this with a secondary graph with the same nodes but different paths. This concept can also be called using a <strong>layered graph</strong>. Here's a code draft for the solution:
    
    [code language="js"]
    import graphlib from 'graphlib';
    
    let costGraph;
    let costMap;
    let pathGraph;
    let pathMap;
    
    buildGraphs(data) {
    const options = { directed: false, compound: false, multigraph: false };
    pathGraph = new graphlib.Graph(options);
    costGraph = new graphlib.Graph(options);
    
    data.paths.forEach((edge) =&gt; {
    pathGraph.setEdge(edge.from, edge.to);
    });
    
    data.costs.forEach((edge) =&gt; {
    costGraph.setEdge(edge.from, edge.to, Number(edge.value));
    });
    
    costMap = graphlib.alg.floydWarshall(
    costGraph,
    (e) =&gt; costGraph.edge(e),
    (e) =&gt; costGraph.nodeEdges(e)
    );
    
    pathMap = graphlib.alg.floydWarshall(
    pathGraph,
    (e) =&gt; 1,
    (e) =&gt; pathGraph.nodeEdges(e)
    );
    }
    
    getPath(from, to) {
    const subMap = pathMap[from];
    const path = [];
    
    path.push(to);
    return buildPath(subMap, path, from, to); //Build path recursively
    }
    
    getCost(from, to) {
    return costMap[from][to].distance;
    }
    [/code]
    
    As you can notice, I created 2 variables called <strong>maps</strong> to store the path computation offered by <strong>graphlib</strong>. This way I can simply query what I need in separate methods keeping the rest of the code clean, if I require to reload graph data I can call <strong>buildGraph</strong> with the data in the format of JSON
    
    [code language="js"]
    {
    paths: [{ from: 'CE', to: 'NA' }, { from: 'CE', to: 'SA' }...]
    costs: [{ from: 'CE', to: 'AF', value: '6.20' }, { from: 'AF', to: 'NA', value: '13.15' }...]
    }
    [/code]
    
    Notice the separation of the chaff from the wheat: the costs are now all associated together in the same graph with discounts included and I kept the paths lean with the only paths allowed.
    <h4>Representation</h4>
    I got tired of drawing illustrations, how about we generate a graph from data? For this I decided to use one of the most powerful graph libraries in the javascript world: <strong>D3</strong>. The best part about D3 is that there are <a href="http://techslides.com/over-1000-d3-js-examples-and-demos"><strong>enough</strong> examples</a> you can use as a first step. Once you have chosen the kind of graph representation you want to use, it also offers a <a href="https://github.com/mbostock/d3/wiki/API-Reference">powerful API</a> to play around with. For this example I will use a <a href="https://github.com/mbostock/d3/wiki/Force-Layout">force directed layout</a>.
    
    Formatting a D3 data file is as easy as formatting a JSON object:
    
    [code language="js"]
    import _ from 'lodash';
    import appRoot from 'app-root-path';
    import fs from 'fs';
    
    exportGraph(graph) {
    
    let formatData = {
    nodes: [],
    links: []
    };
    
    let nodes = graph.nodes;
    let links = graph.edges;
    
    _.forEach(nodes, (row, key) =&gt; {
    formatData.nodes.push({
    name: row.v,
    group: key
    });
    });
    
    _.forEach(links, (row) =&gt; {
    this.format.links.push({
    source: _.find(formatData.nodes, { name:row.v }).group,
    target: _.find(formatData.nodes, { name:row.w }).group,
    value:row.value
    });
    });
    
    fs.writeFile(appRoot + '/' + 'graph.json', JSON.stringify(formatData), function (err) {
    if (err) throw err;
    });
    }
    [/code]
    
    With some help from my <i>friend</i>, <strong>lodash</strong>, the task looks pretty clean.
    
    Finally for the actual frontend code, I got an example from <a href="https://github.com/mbostock/d3/wiki/Force-Layout">the d3 reference repo</a> and tweaked with it a bit, you can run the example I present on my own <a href="https://github.com/JoaoHenriquePereira/graph-example">repo</a> by building the project and pointing a simple server to the index.html in the d3 folder. For example I used a <a href="https://chrome.google.com/webstore/detail/web-server-for-chrome/ofhbbkphhbklhfoeikjpcbhemlocgigb?hl=en">chrome extension</a> for this purpose.
    
    However I left the example unfinished, the paths don't represent correctly our layered graph. It's not that hard to tweak it and it's a fun exercise I'll leave up to you.
    <h3>The fun never ends</h3>
    Sometimes you need to see the application to understand the potential and that's what I aimed at with this post... this is just the tip of the iceberg that is <strong>graph theory</strong>!
    
    Don't be intimidated to search <a>GitHub</a> or even <a href="https://www.google.com/search?q=graph+library">Google</a> for good graph libraries that do all the heavy lifting for you. Many are also well tested even for production use.
    <h3>References:</h3>
    <h4>1 - <a href="https://github.com/JoaoHenriquePereira/graph-example">Repo with a code example</a></h4>
    <h4>2 - <a href="https://github.com/cpettitt/graphlib">Graphlib for javascript</a></h4>
    <h4>3 - <a href="http://d3js.org/">D3.js</a></h4>
fusion_builder_converted:
  - 'yes'
sbg_selected_sidebar:
  - 'a:1:{i:0;s:1:"0";}'
sbg_selected_sidebar_replacement:
  - 'a:1:{i:0;s:12:"Blog Sidebar";}'
sbg_selected_sidebar_2:
  - 'a:1:{i:0;s:1:"0";}'
sbg_selected_sidebar_2_replacement:
  - 'a:1:{i:0;s:0:"";}'
pyre_show_first_featured_image:
  - 'no'
pyre_fimg_width:
  - ""
pyre_fimg_height:
  - ""
pyre_portfolio_width_100:
  - 'no'
pyre_video:
  - ""
pyre_image_rollover_icons:
  - linkzoom
pyre_link_icon_url:
  - ""
pyre_post_links_target:
  - 'no'
pyre_related_posts:
  - default
pyre_share_box:
  - default
pyre_post_pagination:
  - default
pyre_author_info:
  - default
pyre_post_meta:
  - default
pyre_post_comments:
  - 'yes'
pyre_main_top_padding:
  - ""
pyre_main_bottom_padding:
  - ""
pyre_hundredp_padding:
  - ""
pyre_slider_type:
  - 'no'
pyre_slider:
  - "0"
pyre_wooslider:
  - "0"
pyre_revslider:
  - "0"
pyre_elasticslider:
  - "0"
pyre_slider_position:
  - default
pyre_avada_rev_styles:
  - default
pyre_fallback:
  - ""
pyre_demo_slider:
  - ""
pyre_display_header:
  - 'yes'
pyre_header_100_width:
  - default
pyre_header_bg_color:
  - ""
pyre_header_bg_opacity:
  - ""
pyre_header_bg:
  - ""
pyre_header_bg_full:
  - 'no'
pyre_header_bg_repeat:
  - repeat
pyre_displayed_menu:
  - default
pyre_display_footer:
  - default
pyre_display_copyright:
  - default
pyre_footer_100_width:
  - default
pyre_sidebar_position:
  - default
pyre_sidebar_bg_color:
  - ""
pyre_page_bg_layout:
  - default
pyre_page_bg_color:
  - ""
pyre_page_bg:
  - ""
pyre_page_bg_full:
  - 'no'
pyre_page_bg_repeat:
  - repeat
pyre_wide_page_bg_color:
  - ""
pyre_wide_page_bg:
  - ""
pyre_wide_page_bg_full:
  - 'no'
pyre_wide_page_bg_repeat:
  - repeat
pyre_page_title:
  - 'no'
pyre_page_title_breadcrumbs_search_bar:
  - default
pyre_page_title_text:
  - 'yes'
pyre_page_title_text_alignment:
  - default
pyre_page_title_custom_text:
  - ""
pyre_page_title_text_size:
  - ""
pyre_page_title_custom_subheader:
  - ""
pyre_page_title_custom_subheader_text_size:
  - ""
pyre_page_title_font_color:
  - ""
pyre_page_title_100_width:
  - default
pyre_page_title_height:
  - ""
pyre_page_title_mobile_height:
  - ""
pyre_page_title_bar_bg_color:
  - ""
pyre_page_title_bar_borders_color:
  - ""
pyre_page_title_bar_bg:
  - ""
pyre_page_title_bar_bg_retina:
  - ""
pyre_page_title_bar_bg_full:
  - default
pyre_page_title_bg_parallax:
  - default
image: /wp-content/uploads/2015/08/Twitter-network-visualization-social-graph-1024-postbit-1802.jpg
categories:
  - ALL
---
Using tables to store data in a database is so common many developers often apply the same relational-database-voodoo solutions and focus on code architecture instead. It&#8217;s a convenient trap one might fall into when deadlines are tough or little attention is given to the type of information being stored. It&#8217;s amazing how little graphs are considered as a solution to represent data, often perceived as too complex to translate into code.

Ultimately the persistence of graph data translates into a table but the way you handle your data is completely different.

The application of graphs in programming is **huge**, more than the typical minimum distance problems!

### Basics

It is well worth to explore the [mathematical definitions](https://en.wikipedia.org/wiki/Graph_(mathematics)) but I won&#8217;t be covering so deeply every concept. Instead I will present a few simple examples that illustrate how much you can do with so little.

First of all it&#8217;s important to understand what I mean by node graph:

<div  class="fusion-fullwidth fullwidth-box hundred-percent-fullwidth"  style='background-color: #ffffff;background-position: center center;background-repeat: no-repeat;padding-top:0px;padding-right:0px;padding-bottom:0px;padding-left:0px;'>
  <div class="fusion-builder-row fusion-row ">
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <div id="attachment_1358" style="width: 474px" class="wp-caption alignnone">
          <a href="https://codeandunicorns.com/wp-content/uploads/2015/08/undirected.png"><img class="size-full wp-image-1358" src="https://codeandunicorns.com/wp-content/uploads/2015/08/undirected.png" alt="Undirected 3 node graph" width="464" height="245" srcset="https://codeandunicorns.com/wp-content/uploads/2015/08/undirected-300x158.png 300w, https://codeandunicorns.com/wp-content/uploads/2015/08/undirected.png 464w" sizes="(max-width: 464px) 100vw, 464px" /></a>
          
          <p class="wp-caption-text">
            Undirected 3 node graph
          </p>
        </div>
        
        <p>
          Notice the example above is an <strong>undirected graph</strong>, this means it&#8217;s possible to traverse the graph starting on <strong>A</strong> all the way to <strong>B</strong> and vice-versa. This wouldn&#8217;t be the case if we had a <strong>directed graph</strong> instead:
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <div id="attachment_1356" style="width: 474px" class="wp-caption alignnone">
          <a href="https://codeandunicorns.com/wp-content/uploads/2015/08/directed.png"><img class="size-full wp-image-1356" src="https://codeandunicorns.com/wp-content/uploads/2015/08/directed.png" alt="Directed 3 node graph" width="464" height="245" srcset="https://codeandunicorns.com/wp-content/uploads/2015/08/directed-300x158.png 300w, https://codeandunicorns.com/wp-content/uploads/2015/08/directed.png 464w" sizes="(max-width: 464px) 100vw, 464px" /></a>
          
          <p class="wp-caption-text">
            Directed 3 node graph
          </p>
        </div>
        
        <p>
          In this case we have the same graph but once we go from <strong>A</strong> to <strong>B</strong> we can&#8217;t go back! Practically this can be translated to:
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: jscript; title: ; notranslate" title="">
graph -&gt; getEdge('A','B'); //true
graph -&gt; getEdge('B','A'); //undefined
</pre>
        
        <p>
          With <strong>direction</strong> we can define <strong>path constraints</strong>!
        </p>
        
        <h4>
          Distance
        </h4>
        
        <p>
          Say you&#8217;d like to add a value by going through an edge, in that case you are adding a <strong>distance</strong> or simply a <strong>label</strong>. With labels you can describe an <strong>operation</strong>:
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <div id="attachment_1363" style="width: 474px" class="wp-caption alignnone">
          <a href="https://codeandunicorns.com/wp-content/uploads/2015/08/label.png"><img class="size-full wp-image-1363" src="https://codeandunicorns.com/wp-content/uploads/2015/08/label.png" alt="Undirected labeled graph" width="464" height="245" srcset="https://codeandunicorns.com/wp-content/uploads/2015/08/label-300x158.png 300w, https://codeandunicorns.com/wp-content/uploads/2015/08/label.png 464w" sizes="(max-width: 464px) 100vw, 464px" /></a>
          
          <p class="wp-caption-text">
            Undirected labeled graph
          </p>
        </div>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: jscript; title: ; notranslate" title="">
graph -&gt; getEdge('A','B'); //+
graph -&gt; getEdge('B','A'); //+
graph -&gt; getEdge('B','C'); //-
graph -&gt; getEdge('C','B'); //-
</pre>
        
        <p>
          &#8230;similarly with distance values you can add <strong>rates</strong>:
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <div id="attachment_1364" style="width: 474px" class="wp-caption alignnone">
          <a href="https://codeandunicorns.com/wp-content/uploads/2015/08/rate.jpg"><img class="size-full wp-image-1364" src="https://codeandunicorns.com/wp-content/uploads/2015/08/rate.jpg" alt="Undirected weighted graph" width="464" height="245" srcset="https://codeandunicorns.com/wp-content/uploads/2015/08/rate-300x158.jpg 300w, https://codeandunicorns.com/wp-content/uploads/2015/08/rate.jpg 464w" sizes="(max-width: 464px) 100vw, 464px" /></a>
          
          <p class="wp-caption-text">
            Undirected weighted graph
          </p>
        </div>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: jscript; title: ; notranslate" title="">
graph -&gt; getEdge('A','B'); //0.5
graph -&gt; getEdge('B','A'); //0.5
graph -&gt; getEdge('B','C'); //1.2
graph -&gt; getEdge('C','B'); //1.2
</pre>
        
        <h4>
          Multigraphs
        </h4>
        
        <p>
          Multigraphs offer a more broad range of solutions for complex graphs. We simply allow nodes to have more than one edge connecting the same nodes, how? You add a name to the edge of course.
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <div id="attachment_1368" style="width: 465px" class="wp-caption alignnone">
          <a href="https://codeandunicorns.com/wp-content/uploads/2015/08/multi.jpg"><img class="size-full wp-image-1368" src="https://codeandunicorns.com/wp-content/uploads/2015/08/multi.jpg" alt="Undirected 3 node multigraph" width="455" height="323" srcset="https://codeandunicorns.com/wp-content/uploads/2015/08/multi-300x214.jpg 300w, https://codeandunicorns.com/wp-content/uploads/2015/08/multi.jpg 455w" sizes="(max-width: 455px) 100vw, 455px" /></a>
          
          <p class="wp-caption-text">
            Undirected 3 node multigraph
          </p>
        </div>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: jscript; title: ; notranslate" title="">
graph -&gt; getEdge('A','B', 'input'); //ioread
graph -&gt; getEdge('A','B', 'output'); //iowrite
graph -&gt; getEdge('B','C', 'input'); //fileread
graph -&gt; getEdge('B','C', 'output'); //filewrite
</pre>
        
        <p>
          This example is merely illustrative, my point being: if you&#8217;re not used to graph theory I hope by now you start understanding the potential of what you can do if you own a good <strong>graph library</strong>.
        </p>
        
        <p>
          It&#8217;s amazing the amount of times I&#8217;ve seen business logic <strong>hammered</strong> programatically. With graphs you can <strong>hide complexity</strong> and apply clear <strong>business logic</strong> loaded from a database (for example) promoting cleaner code instead of applying long, nested <strong>if</strong> blocks or unending configuration files.
        </p>
        
        <h3>
          Concrete example
        </h3>
        
        <p>
          Before yawns are had I&#8217;ll play a bit with an example and for the sake of it I&#8217;ll use javascript with the cool public <a href="https://github.com/cpettitt/graphlib">graphlib</a>.
        </p>
        
        <p>
          Say we have a worldwide online shop with multiple outposts (1 per continent) and we want to access shipping costs of a package. Before shipping to the customers&#8217; address the package has to first be shipped along to the nearest outpost. The scenario would look something like this:
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <div id="attachment_1378" style="width: 643px" class="wp-caption alignnone">
          <a href="https://codeandunicorns.com/wp-content/uploads/2015/08/Untitled.jpg"><img class="size-full wp-image-1378" src="https://codeandunicorns.com/wp-content/uploads/2015/08/Untitled.jpg" alt="NA - North America SA - South America CE - Central Europe AF - Africa AS - Asia AU - Australia " width="633" height="404" srcset="https://codeandunicorns.com/wp-content/uploads/2015/08/Untitled-300x191.jpg 300w, https://codeandunicorns.com/wp-content/uploads/2015/08/Untitled-460x295.jpg 460w, https://codeandunicorns.com/wp-content/uploads/2015/08/Untitled.jpg 633w" sizes="(max-width: 633px) 100vw, 633px" /></a>
          
          <p class="wp-caption-text">
            NA &#8211; North America<br />SA &#8211; South America<br />CE &#8211; Central Europe<br />AF &#8211; Africa<br />AS &#8211; Asia<br />AU &#8211; Australia
          </p>
        </div>
        
        <p>
          Let also add some prices per trip:
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <div class="table-responsive">
          <table  style="width:100%; "  class="easy-table easy-table-default " border="0">
            <tr>
              <th >
                From
              </th>
              
              <th >
                To
              </th>
              
              <th >
                Value
              </th>
            </tr>
            
            <tr>
              <td >
                CE
              </td>
              
              <td >
                NA
              </td>
              
              <td >
                14.85 $
              </td>
            </tr>
            
            <tr>
              <td >
                CE
              </td>
              
              <td >
                SA
              </td>
              
              <td >
                13.15 $
              </td>
            </tr>
            
            <tr>
              <td >
                CE
              </td>
              
              <td >
                AF
              </td>
              
              <td >
                6.20 $
              </td>
            </tr>
            
            <tr>
              <td >
                CE
              </td>
              
              <td >
                AS
              </td>
              
              <td >
                23.60 $
              </td>
            </tr>
            
            <tr>
              <td >
                SA
              </td>
              
              <td >
                AF
              </td>
              
              <td >
                13.15 $
              </td>
            </tr>
            
            <tr>
              <td >
                AS
              </td>
              
              <td >
                AU
              </td>
              
              <td >
                9.65 $
              </td>
            </tr>
          </table>
        </div>
        
        <p>
          &#8230; this would be a bit boring so lets add a special constraint to spice it up. Our outpost in Africa managed to negotiate a great discount, valid only when shipping to North America. The shipping path stays the same but now we have a price exception.
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <div class="table-responsive">
          <table  style="width:100%; "  class="easy-table easy-table-default " border="0">
            <tr>
              <th >
                From
              </th>
              
              <th >
                To
              </th>
              
              <th >
                Value
              </th>
            </tr>
            
            <tr>
              <td >
                AF
              </td>
              
              <td >
                NA
              </td>
              
              <td >
                13.15 $
              </td>
            </tr>
          </table>
        </div>
        
        <p>
          The problem with the exception is that if we wanted to retrieve the shortest path <strong>and</strong> the lowest cost possible it wouldn&#8217;t work with one graph alone, i.e. if we imported both tables onto our graph via <strong>setEdge()</strong> every time we computed the shortest path between Africa and North America the result would be a direct connection between Africa and North America thus violating our first constraints.
        </p>
        
        <p>
          No biggie we can solve this with a secondary graph with the same nodes but different paths. This concept can also be called using a <strong>layered graph</strong>. Here&#8217;s a code draft for the solution:
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: jscript; title: ; notranslate" title="">
import graphlib from 'graphlib';

let costGraph;
let costMap;
let pathGraph;
let pathMap;

buildGraphs(data) {
  const options = { directed: false, compound: false, multigraph: false };
  pathGraph = new graphlib.Graph(options);
  costGraph = new graphlib.Graph(options);

  data.paths.forEach((edge) =&gt; {
    pathGraph.setEdge(edge.from, edge.to);
  });

  data.costs.forEach((edge) =&gt; {
    costGraph.setEdge(edge.from, edge.to, Number(edge.value));
  });

  costMap = graphlib.alg.floydWarshall(
    costGraph,
    (e) =&gt; costGraph.edge(e),
    (e) =&gt; costGraph.nodeEdges(e)
  );

  pathMap = graphlib.alg.floydWarshall(
    pathGraph,
    (e) =&gt; 1,
    (e) =&gt; pathGraph.nodeEdges(e)
  );
}

getPath(from, to) {
  const subMap = pathMap[from];
  const path = [];

  path.push(to);
  return buildPath(subMap, path, from, to); //Build path recursively
}

getCost(from, to) {
  return costMap[from][to].distance;
}
</pre>
        
        <p>
          As you can notice, I created 2 variables called <strong>maps</strong> to store the path computation offered by <strong>graphlib</strong>. This way I can simply query what I need in separate methods keeping the rest of the code clean, if I require to reload graph data I can call <strong>buildGraph</strong> with the data in the format of JSON
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: jscript; title: ; notranslate" title="">
{
  paths: [{ from: 'CE', to: 'NA' }, { from: 'CE', to: 'SA' }...]
  costs: [{ from: 'CE', to: 'AF', value: '6.20' }, { from: 'AF', to: 'NA', value: '13.15' }...]
}
</pre>
        
        <p>
          Notice the separation of the chaff from the wheat: the costs are now all associated together in the same graph with discounts included and I kept the paths lean with the only paths allowed.
        </p>
        
        <h4>
          Representation
        </h4>
        
        <p>
          I got tired of drawing illustrations, how about we generate a graph from data? For this I decided to use one of the most powerful graph libraries in the javascript world: <strong>D3</strong>. The best part about D3 is that there are <a href="http://techslides.com/over-1000-d3-js-examples-and-demos"><strong>enough</strong> examples</a> you can use as a first step. Once you have chosen the kind of graph representation you want to use, it also offers a <a href="https://github.com/mbostock/d3/wiki/API-Reference">powerful API</a> to play around with. For this example I will use a <a href="https://github.com/mbostock/d3/wiki/Force-Layout">force directed layout</a>.
        </p>
        
        <p>
          Formatting a D3 data file is as easy as formatting a JSON object:
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: jscript; title: ; notranslate" title="">
import _ from 'lodash';
import appRoot from 'app-root-path';
import fs from 'fs';

exportGraph(graph) {

  let formatData = {
    nodes: [],
    links: []
  };

  let nodes = graph.nodes;
  let links = graph.edges;

  _.forEach(nodes, (row, key) =&gt; {
    formatData.nodes.push({
      name: row.v,
      group: key
    });
  });

  _.forEach(links, (row) =&gt; {
    this.format.links.push({
      source: _.find(formatData.nodes, { name:row.v }).group,
      target: _.find(formatData.nodes, { name:row.w }).group,
      value:row.value
    });
  });

  fs.writeFile(appRoot + '/' + 'graph.json', JSON.stringify(formatData), function (err) {
    if (err) throw err;
  });
}
</pre>
        
        <p>
          With some help from my <i>friend</i>, <strong>lodash</strong>, the task looks pretty clean.
        </p>
        
        <p>
          Finally for the actual frontend code, I got an example from <a href="https://github.com/mbostock/d3/wiki/Force-Layout">the d3 reference repo</a> and tweaked with it a bit, you can run the example I present on my own <a href="https://github.com/JoaoHenriquePereira/graph-example">repo</a> by building the project and pointing a simple server to the index.html in the d3 folder. For example I used a <a href="https://chrome.google.com/webstore/detail/web-server-for-chrome/ofhbbkphhbklhfoeikjpcbhemlocgigb?hl=en">chrome extension</a> for this purpose.
        </p>
        
        <p>
          However I left the example unfinished, the paths don&#8217;t represent correctly our layered graph. It&#8217;s not that hard to tweak it and it&#8217;s a fun exercise I&#8217;ll leave up to you.
        </p>
        
        <h3>
          The fun never ends
        </h3>
        
        <p>
          Sometimes you need to see the application to understand the potential and that&#8217;s what I aimed at with this post&#8230; this is just the tip of the iceberg that is <strong>graph theory</strong>!
        </p>
        
        <p>
          Don&#8217;t be intimidated to search <a>GitHub</a> or even <a href="https://www.google.com/search?q=graph+library">Google</a> for good graph libraries that do all the heavy lifting for you. Many are also well tested even for production use.
        </p>
        
        <h3>
          References:
        </h3>
        
        <h4>
          1 &#8211; <a href="https://github.com/JoaoHenriquePereira/graph-example">Repo with a code example</a>
        </h4>
        
        <h4>
          2 &#8211; <a href="https://github.com/cpettitt/graphlib">Graphlib for javascript</a>
        </h4>
        
        <h4>
          3 &#8211; <a href="http://d3js.org/">D3.js</a>
        </h4>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
  </div>
</div>