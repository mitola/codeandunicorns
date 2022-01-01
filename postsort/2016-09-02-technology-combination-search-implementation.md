---
id: 1900
title: Search implementation mini-stack
date: 2016-09-02T05:00:53+00:00
author: Matjaz Trcek
layout: post
guid: https://codeandunicorns.com/?p=1900
permalink: /technology-combination-search-implementation/
slide_template:
  - default
fusion_builder_status:
  - inactive
avada_post_views_count:
  - "2201"
dsq_thread_id:
  - "5111651888"
fusion_builder_content_backup:
  - |
    Recently I was investigating what would be a way of implementing custom search in a CMS I am working at the moment, and part of conclusions was quite interesting and I thought it deserves it's own thought as a minor blog post.
    
    For getting the content scraped from your domains/websites:
    
    <a href="http://scrapy.org/">Scrapy</a> - It provides fairly elegant and quick to implement solutions that help you crawl all the necessary data that you want to index in your search in Python. I was thinking in using it so it scraps everything from www.ANYTHING.com domain for example. Since the output you get is full of RAW HTML and not that easy to make it nicer with only relevant data being left, I included the next addition to the mini-stack.
    
    <a href="https://www.crummy.com/software/BeautifulSoup/bs4/doc/">BeautifulSoup</a> version 4 - A smaller Python lib which makes it great combination with Scrapy. It helps you get that pesky HTML description of the web pages to get something manageable out, like for example the whole text description of the webpage, titles etc...
    
    After we get all the data and Soupify it with the Python soup, it's nice to put it in some kind of DB to make it easier to search for etc. And what's more appropriate then new and flashy....
    
    <a href="https://www.elastic.co/">ElasticSearch</a> - For all the dumped and normalised data we got before, we store everything nicely in ES to make it easier to retrieve.
    
    And now the only thing left on the frontend would be to fetch the data, make appropriate queries to make it relevant to your search specification and voila, you have something kinda manageable for that pesky search that doesn't always work as it should.
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
  - 'no'
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
image: /wp-content/uploads/2016/09/search.jpeg
categories:
  - ALL
---
Recently I was investigating what would be a way of implementing custom search in a CMS I am working at the moment, and part of conclusions was quite interesting and I thought it deserves it&#8217;s own thought as a minor blog post.

For getting the content scraped from your domains/websites:

[Scrapy](http://scrapy.org/) &#8211; It provides fairly elegant and quick to implement solutions that help you crawl all the necessary data that you want to index in your search in Python. I was thinking in using it so it scraps everything from www.ANYTHING.com domain for example. Since the output you get is full of RAW HTML and not that easy to make it nicer with only relevant data being left, I included the next addition to the mini-stack.

[BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/) version 4 &#8211; A smaller Python lib which makes it great combination with Scrapy. It helps you get that pesky HTML description of the web pages to get something manageable out, like for example the whole text description of the webpage, titles etc&#8230;

After we get all the data and Soupify it with the Python soup, it&#8217;s nice to put it in some kind of DB to make it easier to search for etc. And what&#8217;s more appropriate then new and flashy&#8230;.

[ElasticSearch](https://www.elastic.co/) &#8211; For all the dumped and normalised data we got before, we store everything nicely in ES to make it easier to retrieve.

And now the only thing left on the frontend would be to fetch the data, make appropriate queries to make it relevant to your search specification and voila, you have something kinda manageable for that pesky search that doesn&#8217;t always work as it should.