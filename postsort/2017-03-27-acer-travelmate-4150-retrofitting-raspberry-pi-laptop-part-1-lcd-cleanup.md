---
id: 2154
title: 'Acer Travelmate 4150 retrofitting to Raspberry Pi Laptop: Part 1 &#8211; LCD and cleanup'
date: 2017-03-27T14:00:55+00:00
author: Matjaz Trcek
layout: post
guid: https://codeandunicorns.com/?p=2154
permalink: /acer-travelmate-4150-retrofitting-raspberry-pi-laptop-part-1-lcd-cleanup/
slide_template:
  - default
fusion_builder_status:
  - ""
avada_post_views_count:
  - "8109"
dsq_thread_id:
  - "5670266268"
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
image: /wp-content/uploads/2017/03/acer-travelmate-laptop.jpg
categories:
  - ALL
  - Electronics
  - How to
tags:
  - Acer
  - electronics
  - Laptop
  - LCD
  - LVDS
  - raspberry pi 3
---
**First about the idea:** 

I decided to try to create my own laptop with using one of older laptops not useful for anything else. Idea was to find a cheap one on ebay with working LCD and keyboard, ignoring everything else.

**Choosen laptop:**  
Acer Travelmate 4150 15&#8243; Intel Centrino 1.73Ghz spares/rebuild. // Cost 15£

Perfect, It arrived fairly soon and everything seems to be in order. The laptop has only a working LCD and keyboard (possibly touchpad too), but motherboard is fried, which is absolutely fine in this case.

I started with disassembly until I removed power supply, DVD drive, fan, motherboard itself (wohoo, lots of spare parts).  
After that the laptop suddenly transformed into super light shell 😀 it was losing pounds by the hour.

This was the final result:

<img class="aligncenter wp-image-2160 size-large" src="https://codeandunicorns.com/wp-content/uploads/2017/03/acer-travelmate-laptop-dissasembled-768x1024.jpg" alt="Dissasembled Acer laptop for Pi readiness" width="768" height="1024" srcset="https://codeandunicorns.com/wp-content/uploads/2017/03/acer-travelmate-laptop-dissasembled-200x267.jpg 200w, https://codeandunicorns.com/wp-content/uploads/2017/03/acer-travelmate-laptop-dissasembled-225x300.jpg 225w, https://codeandunicorns.com/wp-content/uploads/2017/03/acer-travelmate-laptop-dissasembled-400x534.jpg 400w, https://codeandunicorns.com/wp-content/uploads/2017/03/acer-travelmate-laptop-dissasembled-600x800.jpg 600w, https://codeandunicorns.com/wp-content/uploads/2017/03/acer-travelmate-laptop-dissasembled-768x1024.jpg 768w, https://codeandunicorns.com/wp-content/uploads/2017/03/acer-travelmate-laptop-dissasembled.jpg 800w" sizes="(max-width: 768px) 100vw, 768px" /> 

The first step was completed with this. The second one was figuring out which connector is used by the monitor, and for that I had to investigate quite a lot, and hopefully found the correct one as per the laptops original specification:  
Specification sheet for the LCD: <https://www.manualslib.com/manual/232721/Acer-Travelmate-4150.html?page=45#manual>

Now I have ordered hopefully proper driver and LCD converted for the associated LVDS Connector.

The driver board which seems to be compatible is B150XG01 V2 with controller is:  
[kit for LTN150XB-L03 TV+HDMI+VGA+US<wbr />B LCD LED screen Controller Driver Board](http://www.ebay.co.uk/itm/112217998323?euid=7f448b53378c4611aec61b3ed341e31e&bu=44446927681&cp=1&sojTags=bu=bu)

**Next steps:**  
&#8211; Figure out the most appropriate power supply. One of possibilities would be using Li-ion batteries to which i connect a proper charging circuit. We need to keep in mind that we need to supply power to Raspberry pi 3 (maybe Zero W? , not sure yet) and to LCD converter. Both of them at 12V & 2A, hopefully we can make the battery actually last, or play with different configs without killing the hardware.

&#8211; Make a final connection with LVDS circuit,LCD circuit and the 15&#8243; LCD screen itself.

&#8211; Check how to connect the specific keyboard, or if it is more feasible to chisel laptop a bit more and inserting a custom keyboard is more efficient and logical. because yeah, different keyboards in laptops can act quite differently, sometimes too much manual work is involved.

&nbsp;

<div class="fusion-button-wrapper fusion-aligncenter">
  <a class="fusion-button button-flat fusion-button-round button-large button-default button-7" target="_self" href="https://codeandunicorns.com/acer-travelmate-4150-retrofitting-raspberry-pi-laptop-part-2-working-lcd-raspbian/"><span class="fusion-button-text">CHECK PART 2 HERE</span></a>
</div>