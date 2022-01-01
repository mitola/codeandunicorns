---
id: 1150
title: 'Genomes and object granularity &#8211; II'
date: 2015-06-16T15:05:18+00:00
author: Joao Pereira
layout: post
guid: http://codeandunicorns.com/?p=1150
permalink: /genomes-and-object-granularity-ii/
slide_template:
  - default
pyre_full_width:
  - 'no'
pyre_transparent_header:
  - default
avada_post_views_count:
  - "2033"
fusion_builder_content_backup:
  - |
    As I was finishing the <a href="genomes-and-object-granularity-i/">previous</a> part of these series on computational genomics I couldn't help myself to engage in an actual implementation of a genetic algorithm. But how can one start? Well I tell you... <strong>by doing it</strong>
    
    If you studied operational research the term genetic algorithm shouldn't be a novelty at all. It started as a theory for solving optimisation problems based on an approach (= heuristic) that tries to simulate the process of natural selection. Today it is applied in many fields ranging from computational science to economics.
    
    <strong>TL;DR?</strong> Here's a <a href="https://github.com/JoaoHenriquePereira/rust-tsp">code treat</a> for you.
    
    <h3>We need to go deeper</h3>
    
    Melanie Mitchell makes it <a href="http://www.amazon.com/gp/offer-listing/0262631857/ref=as_li_tl?ie=UTF8&amp;camp=1789&amp;creative=9325&amp;creativeASIN=0262631857&amp;linkCode=am2&amp;tag=codeunico-20&amp;linkId=BSQ7DF6ZLSWUM772">easy</a><img style="border: none !important; margin: 0px !important;" src="http://ir-na.amazon-adsystem.com/e/ir?t=codeunico-20&amp;l=am2&amp;o=1&amp;a=0262631857" alt="" width="1" height="1" border="0" /> for anyone trying to grasp the basics of genetic algorithms:
    <blockquote>
    <ul>
    <li>Start with a randomly generated population of n <i>l-bit</i> chromosomes (candidate solutions to a problem)</li>
    <li>Calculate the fitness f(x) of each chromosomes <i>x</i> in the population.</li>
    <li>Repeat the following steps until n offspring have been created:</li>
    <ul>
    <li>Select a pair of parent chromosomes from the current population, the probability of selection being an increasing function of fitness. Selection is done " with replacement", meaning that the same chromosome can be selected more than once to be come a parent.</li>
    <li>With probability pc (the "crossover probability or "crossover rate"), cross over the pair at randomly chosen point (chosen with uniform probability) to form two offspring. If no crossover takes place, form two offspring that are exact copies of their parents.</li>
    <li>Mutate the two offspring at each locus with probability pm (the mutation probability of mutation rate), and place the resulting chromosomes in the new population. If n is odd, one new population member can be discarded at random.</li>
    
    </ul>
    <li>Replace the current population with the new population.</li>
    <li>Back to step 2.</li>
    </ul>
    </blockquote>
    
    So a basic genetic algorithm seems to have 3 coupled traits: <strong>selection</strong>, <strong>crossover</strong>, <strong>mutation</strong>. Is this enough? Well.. yes to keep it simple of course. We still don't have a problem to solve though, biological cells have been evolving for some time now (say almost 4 billion years!) and they are the true definition of problem solving, just imagine the smallest chemical entity confined in its tiny environment trying to protect itself from extinction. It adapted into huge complexity organisms by using "similar" techniques to spear it's way through the world.
    
    <h3>Real world problems</h3>
    
    <a href="https://codeandunicorns.com/wp-content/uploads/2015/06/the_struggle_is_real.jpg"><img src="https://codeandunicorns.com/wp-content/uploads/2015/06/the_struggle_is_real.jpg" alt="the_struggle_is_real" width="400" height="400" class="alignnone size-full wp-image-1224" style="margin-left:22%;"/></a>
    
    Having a problem to solve is obviously important as it will fill in the context gaps on what is "fitness" and "population" and all other entities involved in a genetic algorithm. I wanted to pick something hard, something meaningful, and oh boy did I? How about a NP-hard problem from the same family of protein folding? At least something understandable and easy to put in words. And <i>voilá</i> the <strong>Travelling Salesman Problem</strong> (<strong>TSP</strong>).
    
    The TSP was formulated around 1930 and has been ever since very effective in provoking migraines and insomnia for mathematical optimisation enthusiasts. There should be a prescription saying it's specially ill advised to think about it when conducting any type of heavy machinery.
    
    But how to explain what a NP problem is? For lack of better explanation I now invite you dear reader to watch the following entertaining clip which showcases the optimisation/complexity zoo:
    
    <iframe width="560" height="315" style="margin-left:10%;" src="https://www.youtube.com/embed/YX40hbAHx3s" frameborder="0" allowfullscreen></iframe>
    
    So we got our problem (yey), now what? Now we need to tell the computer how to doo eet! It's been fruitful already for me to scratch the surface of genetics, why not keeping it going? I was hoping for months for a nice problem to learn <a href="http://www.rust-lang.org/">Rust</a>. Why? Because Rust makes bold promises for systems development, of the likes nobody has dared to make since the very foundation of the C party it grows from. However I'll leave up to you to discover why many are excited about it, there are tons of blog posts about it.
    
    <h3>Let the games begin!</h3>
    
    Starting on coding with a new language while still unsure of the conceptual model was something that itched me immediately. By conceptual model I mean the application of the concept of genetic algorithm to an optimisation problem such as the TSP. As such before actually thinking about the overall source organisation I started by first understanding Rust development and playing around with it. I started laying down the objects required such as GA, population, city and tour. After spending a few (good) hours wrestling the compiler I started to realise that I was seeing the problem the other way around.
    
    My problem is not the GA to solve the TSP, as far as the GA goes all it cares is that whatever uses it follows certain traits, GA is the interface not the object (Duh!). Worse even, I had a singleton graph - "Stop this madness" - I said to myself. But why did I do this? Well first I was just starting with Rust; second, when hacking something together there's this rewarding feeling of an <i>"aha moment"</i> when you realise a way better way of doing it, and so it happened. This concept is loooong known, specially when hacking something around. (PS: find out how/why <a href="http://www.amazon.com/gp/offer-listing/0201835959/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0201835959&linkCode=am2&tag=codeunico-20&linkId=DT7ALT7YIPFDXURJ">here</a><img src="http://ir-na.amazon-adsystem.com/e/ir?t=codeunico-20&l=am2&o=1&a=0201835959" width="1" height="1" border="0" alt="" style="border:none !important; margin:0px !important;" />)
    
    My second attempt was way better, but not yet perfect I confess. You can find the result <a href="https://github.com/JoaoHenriquePereira/rust-tsp">here</a>.
    
    <h3>But wait... there's more!</h3>
    
    If you opened the repo link already you might have noticed there is more than just Rust in the repo. There's also NodeJS! Yep, I wanted to (learn) make my little command line app exposed to the glorious world wide web and I did! It's a simple access layer which uses hypermedia'ish as the engine application state. I say "'ish" as JSON is not exactly a recognised hypermedia format.
    
    At some point I was also playing with MongoDB as a persistence layer but I settled for a simple caching mechanism with <i>node-cache</i>.
    
    <h3>Looking back</h3>
    
    This journey started with genomes and finished with REST api's and solving (yet again!) a travelling salesman problem in Rust. All I have to say is that it has been fun. Surely it's not the best piece of code out there but it features neat constructs which I invite you to take a look:
    
    <ul>
    <li>Rust object JSON serialization/deserialization</li>
    
    [code language="cpp"]
    #[derive(RustcEncodable, RustcDecodable)]
    struct Input {
    graph_type: String,
    graph: Graph,
    options: InputOptions,
    }
    
    #[derive(RustcEncodable, RustcDecodable)]
    struct InputOptions {
    mutation_rate: f64,
    elitism: bool,
    population_size: usize,
    tournament_size: usize,
    }
    
    impl ToJson for Input {
    fn to_json(&amp;self) -&gt; Json {
    let mut d = BTreeMap::new();
    d.insert(&quot;graph_type&quot;.to_string(),
    self.graph_type.to_json());
    d.insert(&quot;graph&quot;.to_string(),
    self.graph.to_json());
    d.insert(&quot;options&quot;.to_string(),
    self.options.to_json());
    Json::Object(d)
    }
    }
    
    impl ToJson for InputOptions {
    fn to_json(&amp;self) -&gt; Json {
    let mut d = BTreeMap::new();
    d.insert(&quot;mutation_rate&quot;.to_string(),
    self.mutation_rate.to_json());
    d.insert(&quot;elitism&quot;.to_string(),
    self.elitism.to_json());
    d.insert(&quot;population_size&quot;.to_string(),
    self.population_size.to_json());
    d.insert(&quot;tournament_size&quot;.to_string(),
    self.tournament_size.to_json());
    Json::Object(d)
    }
    }
    [/code]
    
    <li>Rust/NodeJS communication</li>
    
    [code language="cpp"]
    #[no_mangle]
    pub extern &quot;C&quot; fn compute_adapter(input: *const c_char) -&gt; *const c_char {
    let c_input = unsafe { CStr::from_ptr(input).to_bytes() };
    match str::from_utf8(c_input) {
    Ok(input) =&gt; compute(input),
    Err(e) =&gt; CString::new(e.to_string()).unwrap().as_ptr(),
    }
    }
    
    // Actual handling
    fn compute(input: &amp;str) -&gt; *const c_char {
    //...
    [/code]
    </pre>
    <li>Builder design pattern</li>
    
    [code language="cpp"]
    impl TourBuilder {
    
    /// Constructor for an empty population
    pub fn new() -&gt; TourBuilder {
    TourBuilder {
    tour: Vec::new(),
    fitness: 0.0,
    }
    }
    
    /// Constructor for an empty population with allocated capacity
    pub fn generate_empty_with_size(&amp;mut self, tour_size: usize)
    -&gt; &amp;mut TourBuilder {
    self.tour = Vec::with_capacity(tour_size);
    self
    }
    
    /// Constructor for generating a random tour
    pub fn generate_random_tour(&amp;mut self, mut graph: Graph)
    -&gt; &amp;mut TourBuilder {
    self.tour = graph.get_map();
    thread_rng().shuffle(&amp;mut self.tour);
    self
    }
    
    /// Terminates construction and returns instance
    pub fn finalize(&amp;self) -&gt; Tour {
    Tour {
    tour: self.tour.clone(),
    fitness: self.fitness,
    }
    }
    }
    [/code]
    <li>REST HATEOAS</li>
    
    [code language="javascript"]
    function api_root_get(req, res, next) {
    
    var api_root = new hal.Resource({
    name: pjson.name,
    version: pjson.version,
    repository: pjson.repository,
    cacheable: true
    }, '/'+pjson.name);
    
    api_root.link('compute', '/'+pjson.name+'/compute');
    
    res.send(api_root);
    return next();
    }
    [/code]
    
    <li>Trait interfacing</li>
    
    [code language="cpp"]
    /// Genetic algorithm interface definition
    trait GA {
    fn tournament_selection(&amp;mut self) -&gt; Tour;
    fn crossover(&amp;self, parent_1: Tour, parent_2: Tour) -&gt; Tour;
    fn mutate(&amp;self, tour: Tour) -&gt; Tour;
    }
    
    /// Travelling salesman problem structure definition
    pub struct TSP {
    routes: Population,
    cities: Graph,
    tournament_size: usize,
    mutation_rate: f64,
    _elitism: bool,
    }
    [/code]
    
    </ul>
    
    The project could be adapted to support other algorithms (Simulated annealing anyone?), more graph types or even adding weights/gains to each node in the graphs making it even more interesting.
    
    Before I finish I'd just like to highlight a few points on Rust:
    
    <ul>
    <li><b>It's not an easy language to master</b></li>
    Though I spent a decent amount of time learning Rust I am still far from mastering every concept. Ownership is specially important!
    <li><b>It's not easy to find documentation, but...</b></li>
    Well I was happy enough to use the stable release version from May 2015 and many things have changed, many repos use old deprecated functions and there aren't many great references to learn from, but the community is very good and helpful. Everyone really enjoys the language and provides productive feedback. It can only get better.
    <li><b>The classless (OO'ish) design tends to be clean</b></li>
    Languages such as Go and Rust tend to focus on discipline through enforced compilation rules and making design to an interface and not an implementation. It is still possible to write spaguetti code but at least it's clearer when you do so right from the start. It's not so fun when you just want to hack something together though...
    <li><b>Modules... modules everywhere!</b></li>
    If you pick up Rust, one of your first questions will be: "Ok, what's the best way to organize my code?". Guess what? It has rules that you must follow religiously. In one hand it kind of promotes more structured granularity and code organization. In the other... well... it's bluntly annoying and it feels a bit like an overkill. You can't really have your own preference on this matter, again... it doesn't really promote hacking something together.
    </ul>
    
    <h3>$references</h3>
    <h4>1 - <a href="http://www.amazon.com/gp/offer-listing/0262631857/ref=as_li_tl?ie=UTF8&amp;camp=1789&amp;creative=9325&amp;creativeASIN=0262631857&amp;linkCode=am2&amp;tag=codeunico-20&amp;linkId=BSQ7DF6ZLSWUM772">An Introduction to Genetic Algorithms (Complex Adaptive Systems)</a><img style="border: none !important; margin: 0px !important;" src="http://ir-na.amazon-adsystem.com/e/ir?t=codeunico-20&amp;l=am2&amp;o=1&amp;a=0262631857" alt="" width="1" height="1" border="0" /></h4>
    <h4>2 - <a href="https://en.wikipedia.org/wiki/Evolution_of_cells">The evolution of cells by Wikipedia</a></h4>
    <h4>3 - <a href="https://en.wikipedia.org/wiki/Travelling_salesman_problem">Travelling salesman problem by Wikipedia</a></h4>
    <h4>4 - <a href="https://doc.rust-lang.org/book/">Rust language book</a></h4>
    <h4>5 - <a href="http://www.amazon.com/gp/offer-listing/0201835959/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0201835959&linkCode=am2&tag=codeunico-20&linkId=DT7ALT7YIPFDXURJ">The Mythical Man-Month: Essays on Software Engineering, Anniversary Edition (2nd Edition)</a><img src="http://ir-na.amazon-adsystem.com/e/ir?t=codeunico-20&l=am2&o=1&a=0201835959" width="1" height="1" border="0" alt="" style="border:none !important; margin:0px !important;" />
    </h4>
    
    <h3>Repo</h3>
    <h4>1 - <a href="https://github.com/JoaoHenriquePereira/rust-tsp">TSP solved with genetic algorithm written in Rust</a></h4>
fusion_builder_converted:
  - 'yes'
fusion_builder_status:
  - ""
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
  - default
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
  - default
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
image: /wp-content/uploads/2015/06/11205553_1673673259528102_6329690743620503982_n.jpg
categories:
  - ALL
---
As I was finishing the [previous](genomes-and-object-granularity-i/) part of these series on computational genomics I couldn&#8217;t help myself to engage in an actual implementation of a genetic algorithm. But how can one start? Well I tell you&#8230; **by doing it**

If you studied operational research the term genetic algorithm shouldn&#8217;t be a novelty at all. It started as a theory for solving optimisation problems based on an approach (= heuristic) that tries to simulate the process of natural selection. Today it is applied in many fields ranging from computational science to economics.

**TL;DR?** Here&#8217;s a [code treat](https://github.com/JoaoHenriquePereira/rust-tsp) for you.

### We need to go deeper

Melanie Mitchell makes it [easy](http://www.amazon.com/gp/offer-listing/0262631857/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0262631857&linkCode=am2&tag=codeunico-20&linkId=BSQ7DF6ZLSWUM772)<img style="border: none !important; margin: 0px !important;" src="http://ir-na.amazon-adsystem.com/e/ir?t=codeunico-20&l=am2&o=1&a=0262631857" alt="" width="1" height="1" border="0" /> for anyone trying to grasp the basics of genetic algorithms:

>   * Start with a randomly generated population of n _l-bit_ chromosomes (candidate solutions to a problem)
>   * Calculate the fitness f(x) of each chromosomes _x_ in the population.
>   * Repeat the following steps until n offspring have been created: 
>       * Select a pair of parent chromosomes from the current population, the probability of selection being an increasing function of fitness. Selection is done &#8221; with replacement&#8221;, meaning that the same chromosome can be selected more than once to be come a parent.
>       * With probability pc (the &#8220;crossover probability or &#8220;crossover rate&#8221;), cross over the pair at randomly chosen point (chosen with uniform probability) to form two offspring. If no crossover takes place, form two offspring that are exact copies of their parents.
>       * Mutate the two offspring at each locus with probability pm (the mutation probability of mutation rate), and place the resulting chromosomes in the new population. If n is odd, one new population member can be discarded at random.
>   * Replace the current population with the new population.
>   * Back to step 2.

So a basic genetic algorithm seems to have 3 coupled traits: **selection**, **crossover**, **mutation**. Is this enough? Well.. yes to keep it simple of course. We still don&#8217;t have a problem to solve though, biological cells have been evolving for some time now (say almost 4 billion years!) and they are the true definition of problem solving, just imagine the smallest chemical entity confined in its tiny environment trying to protect itself from extinction. It adapted into huge complexity organisms by using &#8220;similar&#8221; techniques to spear it&#8217;s way through the world.

### Real world problems

[<img class="alignnone size-full wp-image-1224" style="margin-left: 22%;" src="https://codeandunicorns.com/wp-content/uploads/2015/06/the_struggle_is_real.jpg" alt="the_struggle_is_real" width="400" height="400" srcset="https://codeandunicorns.com/wp-content/uploads/2015/06/the_struggle_is_real-66x66.jpg 66w, https://codeandunicorns.com/wp-content/uploads/2015/06/the_struggle_is_real-150x150.jpg 150w, https://codeandunicorns.com/wp-content/uploads/2015/06/the_struggle_is_real-300x300.jpg 300w, https://codeandunicorns.com/wp-content/uploads/2015/06/the_struggle_is_real.jpg 400w" sizes="(max-width: 400px) 100vw, 400px" />](https://codeandunicorns.com/wp-content/uploads/2015/06/the_struggle_is_real.jpg)

Having a problem to solve is obviously important as it will fill in the context gaps on what is &#8220;fitness&#8221; and &#8220;population&#8221; and all other entities involved in a genetic algorithm. I wanted to pick something hard, something meaningful, and oh boy did I? How about a NP-hard problem from the same family of protein folding? At least something understandable and easy to put in words. And _voilá_ the **Travelling Salesman Problem** (**TSP**).

The TSP was formulated around 1930 and has been ever since very effective in provoking migraines and insomnia for mathematical optimisation enthusiasts. There should be a prescription saying it&#8217;s specially ill advised to think about it when conducting any type of heavy machinery.

But how to explain what a NP problem is? For lack of better explanation I now invite you dear reader to watch the following entertaining clip which showcases the optimisation/complexity zoo:



So we got our problem (yey), now what? Now we need to tell the computer how to doo eet! It&#8217;s been fruitful already for me to scratch the surface of genetics, why not keeping it going? I was hoping for months for a nice problem to learn [Rust](http://www.rust-lang.org/). Why? Because Rust makes bold promises for systems development, of the likes nobody has dared to make since the very foundation of the C party it grows from. However I&#8217;ll leave up to you to discover why many are excited about it, there are tons of blog posts about it.

### Let the games begin!

Starting on coding with a new language while still unsure of the conceptual model was something that itched me immediately. By conceptual model I mean the application of the concept of genetic algorithm to an optimisation problem such as the TSP. As such before actually thinking about the overall source organisation I started by first understanding Rust development and playing around with it. I started laying down the objects required such as GA, population, city and tour. After spending a few (good) hours wrestling the compiler I started to realise that I was seeing the problem the other way around.

My problem is not the GA to solve the TSP, as far as the GA goes all it cares is that whatever uses it follows certain traits, GA is the interface not the object (Duh!). Worse even, I had a singleton graph &#8211; &#8220;Stop this madness&#8221; &#8211; I said to myself. But why did I do this? Well first I was just starting with Rust; second, when hacking something together there&#8217;s this rewarding feeling of an _&#8220;aha moment&#8221;_ when you realise a way better way of doing it, and so it happened. This concept is loooong known, specially when hacking something around. (PS: find out how/why [here](http://www.amazon.com/gp/offer-listing/0201835959/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0201835959&linkCode=am2&tag=codeunico-20&linkId=DT7ALT7YIPFDXURJ)<img style="border: none !important; margin: 0px !important;" src="http://ir-na.amazon-adsystem.com/e/ir?t=codeunico-20&l=am2&o=1&a=0201835959" alt="" width="1" height="1" border="0" />)

My second attempt was way better, but not yet perfect I confess. You can find the result [here](https://github.com/JoaoHenriquePereira/rust-tsp).

### But wait&#8230; there&#8217;s more!

If you opened the repo link already you might have noticed there is more than just Rust in the repo. There&#8217;s also NodeJS! Yep, I wanted to (learn) make my little command line app exposed to the glorious world wide web and I did! It&#8217;s a simple access layer which uses hypermedia&#8217;ish as the engine application state. I say &#8220;&#8216;ish&#8221; as JSON is not exactly a recognised hypermedia format.

At some point I was also playing with MongoDB as a persistence layer but I settled for a simple caching mechanism with _node-cache_.

### Looking back

This journey started with genomes and finished with REST api&#8217;s and solving (yet again!) a travelling salesman problem in Rust. All I have to say is that it has been fun. Surely it&#8217;s not the best piece of code out there but it features neat constructs which I invite you to take a look:

  * Rust object JSON serialization/deserialization

<div  class="fusion-fullwidth fullwidth-box hundred-percent-fullwidth"  style='background-color: #ffffff;background-position: center center;background-repeat: no-repeat;padding-top:0px;padding-right:0px;padding-bottom:0px;padding-left:0px;'>
  <div class="fusion-builder-row fusion-row ">
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: cpp; title: ; notranslate" title="">
#[derive(RustcEncodable, RustcDecodable)]
struct Input {
	graph_type: String,
	graph: Graph,
	options: InputOptions,
}

#[derive(RustcEncodable, RustcDecodable)]
struct InputOptions {
	mutation_rate: f64,
	elitism: bool,
	population_size: usize,
	tournament_size: usize,
}

impl ToJson for Input {
    fn to_json(&self) -&gt; Json {
        let mut d = BTreeMap::new();
        d.insert("graph_type".to_string(), 
                self.graph_type.to_json());
        d.insert("graph".to_string(), 
                self.graph.to_json());
        d.insert("options".to_string(), 
                self.options.to_json());
        Json::Object(d)
    }
}

impl ToJson for InputOptions {
    fn to_json(&self) -&gt; Json {
        let mut d = BTreeMap::new();
        d.insert("mutation_rate".to_string(), 
                self.mutation_rate.to_json());
        d.insert("elitism".to_string(), 
                self.elitism.to_json());
        d.insert("population_size".to_string(), 
                self.population_size.to_json());
        d.insert("tournament_size".to_string(), 
                self.tournament_size.to_json());
        Json::Object(d)
    }
}
</pre>
        
        <p>
          &nbsp;
        </p>
        
        <ul>
          <li>
            Rust/NodeJS communication
          </li>
        </ul>
        
        <p>
          &nbsp;
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: cpp; title: ; notranslate" title="">
#[no_mangle]
pub extern "C" fn compute_adapter(input: *const c_char) -&gt; *const c_char {
    let c_input = unsafe { CStr::from_ptr(input).to_bytes() };
    match str::from_utf8(c_input) {
        Ok(input) =&gt; compute(input),
        Err(e) =&gt; CString::new(e.to_string()).unwrap().as_ptr(),
    }
}

// Actual handling
fn compute(input: &str) -&gt; *const c_char {
//...
</pre>
        
        <p>
          &nbsp;
        </p>
        
        <ul>
          <li>
            Builder design pattern
          </li>
        </ul>
        
        <p>
          &nbsp;
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: cpp; title: ; notranslate" title="">
impl TourBuilder {

    /// Constructor for an empty population
    pub fn new() -&gt; TourBuilder {
        TourBuilder {
            tour: Vec::new(),
            fitness: 0.0,
	}
    }

    /// Constructor for an empty population with allocated capacity
    pub fn generate_empty_with_size(&mut self, tour_size: usize) 
        -&gt; &mut TourBuilder {
        self.tour = Vec::with_capacity(tour_size);
        self
    }

    /// Constructor for generating a random tour
    pub fn generate_random_tour(&mut self, mut graph: Graph) 
        -&gt; &mut TourBuilder {
        self.tour = graph.get_map();
        thread_rng().shuffle(&mut self.tour);
        self
    }

    /// Terminates construction and returns instance
    pub fn finalize(&self) -&gt; Tour {
        Tour { 
        	tour: self.tour.clone(),
        	fitness: self.fitness,
        }
    }
}
</pre>
        
        <p>
          &nbsp;
        </p>
        
        <ul>
          <li>
            REST HATEOAS
          </li>
        </ul>
        
        <p>
          &nbsp;
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: jscript; title: ; notranslate" title="">
function api_root_get(req, res, next) {

    var api_root = new hal.Resource({
                    name: pjson.name,
		    version: pjson.version,
		    repository: pjson.repository,
		    cacheable: true
    }, '/'+pjson.name);

    api_root.link('compute', '/'+pjson.name+'/compute');

    res.send(api_root);
    return next();
}
</pre>
        
        <p>
          &nbsp;
        </p>
        
        <ul>
          <li>
            Trait interfacing
          </li>
        </ul>
        
        <p>
          &nbsp;
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: cpp; title: ; notranslate" title="">
/// Genetic algorithm interface definition
trait GA {
    fn tournament_selection(&mut self) -&gt; Tour;
    fn crossover(&self, parent_1: Tour, parent_2: Tour) -&gt; Tour;
    fn mutate(&self, tour: Tour) -&gt; Tour;
}

/// Travelling salesman problem structure definition
pub struct TSP {
    routes: Population,
    cities: Graph,
    tournament_size: usize,
    mutation_rate: f64,
    _elitism: bool,
}
</pre>
        
        <p>
          The project could be adapted to support other algorithms (Simulated annealing anyone?), more graph types or even adding weights/gains to each node in the graphs making it even more interesting.
        </p>
        
        <p>
          Before I finish I&#8217;d just like to highlight a few points on Rust:
        </p>
        
        <ul>
          <ul>
            <li>
              <b>It&#8217;s not an easy language to master</b>
            </li>
          </ul>
        </ul>
        
        <p>
          Though I spent a decent amount of time learning Rust I am still far from mastering every concept. Ownership is specially important!
        </p>
        
        <ul>
          <ul>
            <li>
              <b>It&#8217;s not easy to find documentation, but&#8230;</b>
            </li>
          </ul>
        </ul>
        
        <p>
          Well I was happy enough to use the stable release version from May 2015 and many things have changed, many repos use old deprecated functions and there aren&#8217;t many great references to learn from, but the community is very good and helpful. Everyone really enjoys the language and provides productive feedback. It can only get better.
        </p>
        
        <ul>
          <ul>
            <li>
              <b>The classless (OO&#8217;ish) design tends to be clean</b>
            </li>
          </ul>
        </ul>
        
        <p>
          Languages such as Go and Rust tend to focus on discipline through enforced compilation rules and making design to an interface and not an implementation. It is still possible to write spaguetti code but at least it&#8217;s clearer when you do so right from the start. It&#8217;s not so fun when you just want to hack something together though&#8230;
        </p>
        
        <ul>
          <ul>
            <li>
              <b>Modules&#8230; modules everywhere!</b>
            </li>
          </ul>
        </ul>
        
        <p>
          If you pick up Rust, one of your first questions will be: &#8220;Ok, what&#8217;s the best way to organize my code?&#8221;. Guess what? It has rules that you must follow religiously. In one hand it kind of promotes more structured granularity and code organization. In the other&#8230; well&#8230; it&#8217;s bluntly annoying and it feels a bit like an overkill. You can&#8217;t really have your own preference on this matter, again&#8230; it doesn&#8217;t really promote hacking something together.
        </p>
        
        <h3>
          $references
        </h3>
        
        <h4>
          1 &#8211; <a href="http://www.amazon.com/gp/offer-listing/0262631857/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0262631857&linkCode=am2&tag=codeunico-20&linkId=BSQ7DF6ZLSWUM772">An Introduction to Genetic Algorithms (Complex Adaptive Systems)</a><img style="border: none !important; margin: 0px !important;" src="http://ir-na.amazon-adsystem.com/e/ir?t=codeunico-20&l=am2&o=1&a=0262631857" alt="" width="1" height="1" border="0" />
        </h4>
        
        <h4>
          2 &#8211; <a href="https://en.wikipedia.org/wiki/Evolution_of_cells">The evolution of cells by Wikipedia</a>
        </h4>
        
        <h4>
          3 &#8211; <a href="https://en.wikipedia.org/wiki/Travelling_salesman_problem">Travelling salesman problem by Wikipedia</a>
        </h4>
        
        <h4>
          4 &#8211; <a href="https://doc.rust-lang.org/book/">Rust language book</a>
        </h4>
        
        <h4>
          5 &#8211; <a href="http://www.amazon.com/gp/offer-listing/0201835959/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0201835959&linkCode=am2&tag=codeunico-20&linkId=DT7ALT7YIPFDXURJ">The Mythical Man-Month: Essays on Software Engineering, Anniversary Edition (2nd Edition)</a><img style="border: none !important; margin: 0px !important;" src="http://ir-na.amazon-adsystem.com/e/ir?t=codeunico-20&l=am2&o=1&a=0201835959" alt="" width="1" height="1" border="0" />
        </h4>
        
        <h3>
          Repo
        </h3>
        
        <h4>
          1 &#8211; <a href="https://github.com/JoaoHenriquePereira/rust-tsp">TSP solved with genetic algorithm written in Rust</a>
        </h4>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
  </div>
</div>