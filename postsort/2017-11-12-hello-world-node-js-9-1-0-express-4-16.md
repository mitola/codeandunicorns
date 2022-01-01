---
id: 2306
title: 'Hello world with Node.JS 9.1.0 &#038; Express 4.16.*'
date: 2017-11-12T16:43:58+00:00
author: Matjaz Trcek
layout: post
guid: https://codeandunicorns.com/?p=2306
permalink: /hello-world-node-js-9-1-0-express-4-16/
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
  - default
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
pyre_slider_type:
  - 'no'
pyre_slider:
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
pyre_main_top_padding:
  - ""
pyre_main_bottom_padding:
  - ""
pyre_hundredp_padding:
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
pyre_sidebar_sticky:
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
  - default
pyre_page_title_breadcrumbs_search_bar:
  - default
pyre_page_title_text:
  - default
pyre_page_title_text_alignment:
  - default
pyre_page_title_custom_text:
  - ""
pyre_page_title_text_size:
  - ""
pyre_page_title_line_height:
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
fusion_builder_status:
  - ""
kd_featured-image-2_post_id:
  - ""
kd_featured-image-3_post_id:
  - ""
kd_featured-image-4_post_id:
  - ""
kd_featured-image-5_post_id:
  - ""
avada_post_views_count:
  - "4837"
dsq_thread_id:
  - "6279462228"
sbg_selected_sidebar:
  - 'a:1:{i:0;s:1:"0";}'
sbg_selected_sidebar_replacement:
  - 'a:1:{i:0;s:12:"Blog Sidebar";}'
sbg_selected_sidebar_2:
  - 'a:1:{i:0;s:1:"0";}'
sbg_selected_sidebar_2_replacement:
  - 'a:1:{i:0;s:0:"";}'
image: /wp-content/uploads/2017/11/node-express.png
categories:
  - ALL
  - How to
  - The Code
---
Sometimes, when you are picking up a new piece of tech it&#8217;s hard to get started in it, since some of the things can be quite different to what you are used. The following article and the one that will follow are meant to provide as straightforward solutions as possible, with Github code examples that you can download. All the code example will try to reference the versions or most up to date versions as possible. If you notice an outdated version do feel free to fire up an issue on Github or submit a PR with a fix on it. However for this one there won&#8217;t be Github example since it&#8217;s really basic, and it&#8217;s good to know by heart how to make the simplest of Node.js configs.

Introduction to basic installation of newest Node.JS and Express:

<img class="aligncenter wp-image-2308 size-full" title="node js install image" src="https://codeandunicorns.com/wp-content/uploads/2017/11/nodejs_install-min.png" alt="" width="800" height="564" srcset="https://codeandunicorns.com/wp-content/uploads/2017/11/nodejs_install-min-200x141.png 200w, https://codeandunicorns.com/wp-content/uploads/2017/11/nodejs_install-min-300x212.png 300w, https://codeandunicorns.com/wp-content/uploads/2017/11/nodejs_install-min-400x282.png 400w, https://codeandunicorns.com/wp-content/uploads/2017/11/nodejs_install-min-600x423.png 600w, https://codeandunicorns.com/wp-content/uploads/2017/11/nodejs_install-min-768x541.png 768w, https://codeandunicorns.com/wp-content/uploads/2017/11/nodejs_install-min.png 800w" sizes="(max-width: 800px) 100vw, 800px" /> 

1.) Install Node.JS. Go to: <https://nodejs.org/en/> and choose 9.1.0 or the latest Current version. After downloads finishes Install it and just follow the instructions.

2.) Go to your desired project folder and write following commands:

For creation of your project folder and cd-ing into it.  
`mkdir myapp<br />
cd myapp`

This will initialize your package.json. Follow the questions and fill out the info  
`npm init`

3.) When getting prompted for entry point, write index.js instead.

4.) After you finish the init, add express to the list of dependencies:

`npm install express --save`

5.) In index.js file that you pointed to, and created it, add the following:

`<br />
const express = require('express')<br />
const app = express()`

app.get(&#8216;/&#8217;, (req, res) => res.send(&#8216;Hello World!&#8217;))

app.listen(3000, () => console.log(&#8216;Example app listening on port 3000!&#8217;))

6.) Congrats.

Run:

After following all the previous steps  
`node index.js`

and go to [http://localhost:3000/](localhost:3000/)

At this point your local machine should have the server setup and running on the above url. You should see a Hello world displaying back at you.