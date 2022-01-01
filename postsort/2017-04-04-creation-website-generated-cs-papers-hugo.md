---
id: 2169
title: 'Creation of website &#8211; Generated CS Papers with Hugo'
date: 2017-04-04T15:19:39+00:00
author: Matjaz Trcek
layout: post
guid: https://codeandunicorns.com/?p=2169
permalink: /creation-website-generated-cs-papers-hugo/
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
avada_post_views_count:
  - "1896"
dsq_thread_id:
  - "5695294544"
image: /wp-content/uploads/2017/04/404page.jpg
categories:
  - ALL
---
I have been playing recently with Static website generators such as Jekyll and Hugo.

I wanted to do a quick demo mostly for myself to see it&#8217;s performance and how it all ties together in a sense of structure and development.

The following page: <https://generatedcspapers.codeandunicorns.com/> is made with [Hugo](https://gohugo.io/).

DOMContentLoad takes approximately 172ms and Load in Chrome inspect around 246ms, with all together 3 requests, the website itself is around 14kb as in just the HTML designy part. That&#8217;s pretty impressive, of course the biggest part of the load of the websites in this case will be any JS that you will be adding for the future. Regarding articles themselves, I was checking into usage of [SCIgen &#8211; An Automatic CS Paper Generator](https://pdos.csail.mit.edu/archive/scigen/). It is quite an awesome thing, it created automatically generate CS academia like papers, that are pretty much BS more or less, but at the same time the structure, and the feel is that it is correct-ish.  
<img class="aligncenter wp-image-2170 size-large" src="https://codeandunicorns.com/wp-content/uploads/2017/04/mainCSgeneratedpaperssite-1024x510.jpg" alt="" width="1024" height="510" srcset="https://codeandunicorns.com/wp-content/uploads/2017/04/mainCSgeneratedpaperssite-200x100.jpg 200w, https://codeandunicorns.com/wp-content/uploads/2017/04/mainCSgeneratedpaperssite-300x149.jpg 300w, https://codeandunicorns.com/wp-content/uploads/2017/04/mainCSgeneratedpaperssite-400x199.jpg 400w, https://codeandunicorns.com/wp-content/uploads/2017/04/mainCSgeneratedpaperssite-600x299.jpg 600w, https://codeandunicorns.com/wp-content/uploads/2017/04/mainCSgeneratedpaperssite-768x382.jpg 768w, https://codeandunicorns.com/wp-content/uploads/2017/04/mainCSgeneratedpaperssite-800x398.jpg 800w, https://codeandunicorns.com/wp-content/uploads/2017/04/mainCSgeneratedpaperssite-1024x510.jpg 1024w, https://codeandunicorns.com/wp-content/uploads/2017/04/mainCSgeneratedpaperssite-1200x598.jpg 1200w, https://codeandunicorns.com/wp-content/uploads/2017/04/mainCSgeneratedpaperssite.jpg 1500w" sizes="(max-width: 1024px) 100vw, 1024px" /> 

Theme that I used with Hugo is called [After Dark](http://themes.gohugo.io/after-dark/) and is very heavily performance optimised, but a nice thing is that it provides out of box support with very simple one liners to add Disqus and Google Analytics with just adding the unique identifiers to config.toml file. The theme also features on the overview list an amazing time reader, which I love, but am not sure why exactly.

Regarding the static generators like Hugo:

It is super high performant, but creation of content is not as user/editor friendly as some of other site creation thingies such as WordPress. But, I do think I saw some offline Hugo or Jekyll CMS with which you can create content locally in more user/GUI friendly way. I am totally fine with writing Markdown format, but for some people it may be easier to take a look into that as well. But due to Hugo being what it is, I&#8217;d certainly say it is similar to AMP in a sense, that it semi-limits you what you can actually develop with it, since if you want to high super high performance you are inherently limited in what kind of rich content you want to create, or at least you need to take a look at it from a different direction.

Markdown files as content creation are quite simple with for example \*\*TITLE\*\* marking something as a title and you can easily add any custom HTML for things that you aren&#8217;t able to do with this kind of templating.

Hopefully someone finds the overview interesting, but if you want some more data on performance load times or DOM&#8217;s just ping me and i&#8217;ll update it 🙂