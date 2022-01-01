---
id: 1903
title: PiBakery example of Raspbian setup on boot
date: 2016-09-07T16:53:52+00:00
author: Matjaz Trcek
layout: post
guid: https://codeandunicorns.com/?p=1903
permalink: /pibakery-example-raspbian-setup-boot/
slide_template:
  - default
fusion_builder_status:
  - inactive
avada_post_views_count:
  - "6455"
dsq_thread_id:
  - "5126487815"
fusion_builder_content_backup:
  - |
    <strong><a href="http://www.pibakery.org/index.html">About PiBakery :</a></strong>
    
    PiBakery is a Scratch style program that helps you with pre-setup of Raspbian images. For everyone working often with Raspberry Pi's and creating new images of the system, re-installing system lots of times,  will notice it can be sometimes a bit hard and problematic to keep everything properly up to date. And in this case PiBakery really comes in handy with it's block based structure
    
    So after the short introduction, lets dive into it:
    
    &nbsp;
    
    <img class="aligncenter wp-image-1909 size-large" src="https://codeandunicorns.com/wp-content/uploads/2016/09/Screen-Shot-2016-09-07-at-14.56.27-1024x776.png" alt="pibaker4" width="669" height="507" />
    
    Sample of the new interface screen. Different blocks that you can use are categorized on the left side with ability to import, export you configurations in the upper right part of the interface.
    
    When you create your preconfigured scheme you will be ready to click Write and create your new image.
    
    <img class="aligncenter wp-image-1908 size-full" src="https://codeandunicorns.com/wp-content/uploads/2016/09/Screen-Shot-2016-09-07-at-15.32.59.png" alt="pibaker3" width="892" height="862" />
    
    I have created a short example of the First boot and every boot scripts through which i'll guide you now.
    
    I am using Raspberry pi version 3 therefore The first block after startup is to connect to WiFi via your desired network SSID, pass and encryption.
    
    After the WIFI setup, i run synaptic apt-get install to get the package manager which i personally prefer.
    
    After that running apt-get for Raspbian update and upgrade to update to the newest version of the raspberry and all the bug fixes, etc.
    
    On finishing all of that we install VNC server with your preferred pass to let you connect via VNC to hack and create on your raspberry through remote desktop as I much prefer to do.
    <img class="aligncenter wp-image-1907 size-full" src="https://codeandunicorns.com/wp-content/uploads/2016/09/Screen-Shot-2016-09-07-at-15.33.18.png" alt="pibaker2" width="930" height="472" />
    
    &nbsp;
    
    Following that, let's not forget to change the pass to our preferred one, and setting the boot option to either terminal or Desktop. In my case I do like to use the GUI and mostly using it for home related hacking so no need for too much security, for now.
    
    <img class="aligncenter wp-image-1906 size-large" src="https://codeandunicorns.com/wp-content/uploads/2016/09/Screen-Shot-2016-09-07-at-15.33.29-1024x494.png" alt="pibaker1" width="669" height="323" />
    
    &nbsp;
    
    At the end a short part for On Every boot block. Here I have only added a Run VNC server on the Raspberry, since after every startup it makes it easier to simply connect via GUI.
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
image: /wp-content/uploads/2016/09/Screen-Shot-2016-09-07-at-14.55.15-e1473263687959.png
categories:
  - ALL
---
**[About PiBakery :](http://www.pibakery.org/index.html)**

PiBakery is a Scratch style program that helps you with pre-setup of Raspbian images. For everyone working often with Raspberry Pi&#8217;s and creating new images of the system, re-installing system lots of times,  will notice it can be sometimes a bit hard and problematic to keep everything properly up to date. And in this case PiBakery really comes in handy with it&#8217;s block based structure

So after the short introduction, lets dive into it:

&nbsp;

<img class="aligncenter wp-image-1909 size-large" src="https://codeandunicorns.com/wp-content/uploads/2016/09/Screen-Shot-2016-09-07-at-14.56.27-1024x776.png" alt="pibaker4" width="669" height="507" srcset="https://codeandunicorns.com/wp-content/uploads/2016/09/Screen-Shot-2016-09-07-at-14.56.27-300x227.png 300w, https://codeandunicorns.com/wp-content/uploads/2016/09/Screen-Shot-2016-09-07-at-14.56.27-768x582.png 768w, https://codeandunicorns.com/wp-content/uploads/2016/09/Screen-Shot-2016-09-07-at-14.56.27-1024x776.png 1024w, https://codeandunicorns.com/wp-content/uploads/2016/09/Screen-Shot-2016-09-07-at-14.56.27.png 1266w" sizes="(max-width: 669px) 100vw, 669px" /> 

Sample of the new interface screen. Different blocks that you can use are categorized on the left side with ability to import, export you configurations in the upper right part of the interface.

When you create your preconfigured scheme you will be ready to click Write and create your new image.

<img class="aligncenter wp-image-1908 size-full" src="https://codeandunicorns.com/wp-content/uploads/2016/09/Screen-Shot-2016-09-07-at-15.32.59.png" alt="pibaker3" width="892" height="862" srcset="https://codeandunicorns.com/wp-content/uploads/2016/09/Screen-Shot-2016-09-07-at-15.32.59-52x50.png 52w, https://codeandunicorns.com/wp-content/uploads/2016/09/Screen-Shot-2016-09-07-at-15.32.59-300x290.png 300w, https://codeandunicorns.com/wp-content/uploads/2016/09/Screen-Shot-2016-09-07-at-15.32.59-768x742.png 768w, https://codeandunicorns.com/wp-content/uploads/2016/09/Screen-Shot-2016-09-07-at-15.32.59.png 892w" sizes="(max-width: 892px) 100vw, 892px" /> 

I have created a short example of the First boot and every boot scripts through which i&#8217;ll guide you now.

I am using Raspberry pi version 3 therefore The first block after startup is to connect to WiFi via your desired network SSID, pass and encryption.

After the WIFI setup, i run synaptic apt-get install to get the package manager which i personally prefer.

After that running apt-get for Raspbian update and upgrade to update to the newest version of the raspberry and all the bug fixes, etc.

On finishing all of that we install VNC server with your preferred pass to let you connect via VNC to hack and create on your raspberry through remote desktop as I much prefer to do.  
<img class="aligncenter wp-image-1907 size-full" src="https://codeandunicorns.com/wp-content/uploads/2016/09/Screen-Shot-2016-09-07-at-15.33.18.png" alt="pibaker2" width="930" height="472" srcset="https://codeandunicorns.com/wp-content/uploads/2016/09/Screen-Shot-2016-09-07-at-15.33.18-300x152.png 300w, https://codeandunicorns.com/wp-content/uploads/2016/09/Screen-Shot-2016-09-07-at-15.33.18-768x390.png 768w, https://codeandunicorns.com/wp-content/uploads/2016/09/Screen-Shot-2016-09-07-at-15.33.18.png 930w" sizes="(max-width: 930px) 100vw, 930px" /> 

&nbsp;

Following that, let&#8217;s not forget to change the pass to our preferred one, and setting the boot option to either terminal or Desktop. In my case I do like to use the GUI and mostly using it for home related hacking so no need for too much security, for now.

<img class="aligncenter wp-image-1906 size-large" src="https://codeandunicorns.com/wp-content/uploads/2016/09/Screen-Shot-2016-09-07-at-15.33.29-1024x494.png" alt="pibaker1" width="669" height="323" srcset="https://codeandunicorns.com/wp-content/uploads/2016/09/Screen-Shot-2016-09-07-at-15.33.29-300x145.png 300w, https://codeandunicorns.com/wp-content/uploads/2016/09/Screen-Shot-2016-09-07-at-15.33.29-768x370.png 768w, https://codeandunicorns.com/wp-content/uploads/2016/09/Screen-Shot-2016-09-07-at-15.33.29-1024x494.png 1024w, https://codeandunicorns.com/wp-content/uploads/2016/09/Screen-Shot-2016-09-07-at-15.33.29.png 1282w" sizes="(max-width: 669px) 100vw, 669px" /> 

&nbsp;

At the end a short part for On Every boot block. Here I have only added a Run VNC server on the Raspberry, since after every startup it makes it easier to simply connect via GUI.