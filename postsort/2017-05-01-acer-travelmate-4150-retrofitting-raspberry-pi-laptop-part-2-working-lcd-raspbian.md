---
title: 'Acer Travelmate 4150 retrofitting to Raspberry Pi Laptop: Part 2 – Working LCD and Raspbian'
date: 2017-05-01T14:48:59+00:00
author: Matjaz Trcek
layout: post
guid: https://codeandunicorns.com/?p=2215
permalink: /acer-travelmate-4150-retrofitting-raspberry-pi-laptop-part-2-working-lcd-raspbian/
fusion_builder_status:
  - ""
avada_post_views_count:
  - "4277"
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
dsq_thread_id:
  - "5776209728"
image: /wp-content/uploads/2017/04/acertravelmatedisplayworking.jpg
categories:
  - ALL
---
## Explanation on setup

I finally got the LCD LED controller. I spent some time to understand a bit better how it works. So basically from the LCD controller there is a connector with red/yellow/black lines going to driver board, which is needed for this old types of LCD monitors. From there it is connected with two cables to monitor itself.

The cable covered in black thicker part which combines several cables blue-whites and red ones, goes to the back of LCD display as can be seen on the picture lower down.  This LCD controller also features a really neat control panel with which you can change the channel (HDMI,VGA etc.), change brightness, and all the casual things you may care about more then me.

And there is a normal size HDMI cable connected to Raspberry Pi 3 and LCD controller. The configuration needed which is fairly straightforward is described bellow.

<img class="aligncenter wp-image-2219 size-large" src="https://codeandunicorns.com/wp-content/uploads/2017/04/insideofacertravelmate-1024x768.jpg" alt="" width="1024" height="768" srcset="https://codeandunicorns.com/wp-content/uploads/2017/04/insideofacertravelmate-200x150.jpg 200w, https://codeandunicorns.com/wp-content/uploads/2017/04/insideofacertravelmate-300x225.jpg 300w, https://codeandunicorns.com/wp-content/uploads/2017/04/insideofacertravelmate-400x300.jpg 400w, https://codeandunicorns.com/wp-content/uploads/2017/04/insideofacertravelmate-600x450.jpg 600w, https://codeandunicorns.com/wp-content/uploads/2017/04/insideofacertravelmate-768x576.jpg 768w, https://codeandunicorns.com/wp-content/uploads/2017/04/insideofacertravelmate-800x600.jpg 800w, https://codeandunicorns.com/wp-content/uploads/2017/04/insideofacertravelmate-1024x768.jpg 1024w, https://codeandunicorns.com/wp-content/uploads/2017/04/insideofacertravelmate-1200x900.jpg 1200w, https://codeandunicorns.com/wp-content/uploads/2017/04/insideofacertravelmate.jpg 1601w" sizes="(max-width: 1024px) 100vw, 1024px" /> 

Something I&#8217;d really like to add here on practically and as well difficulty of the build is  that as a concept it is a very good idea, this mini project of mine, but I think at the end there may be quite a bit of problem fitting everything together, my biggest worry being the battery fitting in the case.

But if we look positively at it, LCD controller needs 12 and Rpi 5V. Optimally if you want to make life yourself easier (and reuse the battery pack if needed another time.) I went for 30000 mah battery pack that has 1 DC in 1 DC out (for charging the pack and output to LCD controller) and USB connector for raspberry pi. The choosen battery pack has: Output: DC 12V(5A MAX),16V(3.75A MAX),19V(3.15A MAX), USB1 5V/2.1A  and USB2 5V/1A.

Which means it&#8217;s absolutely perfect. Higher amperage and voltage could be useful with another project and 2A 5V output is perfect for raspberry and 1A i guess you could use for charging something else such as maybe a phone or whatever.

At the moment I am in progress of trying to figure out the best way to connect the default keyboard, cause i am afraid I damaged it in the process of trying to hook it up. As an alternative I can always go bluetooth, but i&#8217;ll try to figure out a solution for it. Also on the [Hacker news thread](https://news.ycombinator.com/item?id=13967312) there were some good suggestions with discovery program on linux to configure a keyboard after you are able to hook it up.

Also while doing this particular project I noticed the amount of spare parts i have in general, and came to an awesome idea of making so called &#8220;Booktop&#8221;. Taking a bit bigger then 7 inch book with hard covers, cutting the paper a bit, insert TFT screen with raspberry Pi Zero W and small LCD controller inside, and adding a Bluetooth keyboard on the other side of the book. Voila, all of the sudden you have book on the outside, but whole world of information on the inside.

<img class="aligncenter wp-image-2225 size-large" src="https://codeandunicorns.com/wp-content/uploads/2017/04/LVDS_laptop_connected-1024x768.jpg" alt="" width="1024" height="768" srcset="https://codeandunicorns.com/wp-content/uploads/2017/04/LVDS_laptop_connected-200x150.jpg 200w, https://codeandunicorns.com/wp-content/uploads/2017/04/LVDS_laptop_connected-300x225.jpg 300w, https://codeandunicorns.com/wp-content/uploads/2017/04/LVDS_laptop_connected-400x300.jpg 400w, https://codeandunicorns.com/wp-content/uploads/2017/04/LVDS_laptop_connected-600x450.jpg 600w, https://codeandunicorns.com/wp-content/uploads/2017/04/LVDS_laptop_connected-768x576.jpg 768w, https://codeandunicorns.com/wp-content/uploads/2017/04/LVDS_laptop_connected-800x600.jpg 800w, https://codeandunicorns.com/wp-content/uploads/2017/04/LVDS_laptop_connected-1024x768.jpg 1024w, https://codeandunicorns.com/wp-content/uploads/2017/04/LVDS_laptop_connected-1200x900.jpg 1200w, https://codeandunicorns.com/wp-content/uploads/2017/04/LVDS_laptop_connected.jpg 1500w" sizes="(max-width: 1024px) 100vw, 1024px" /> 

## **Raspberry pi preparation**

For preparation of Raspbian image I have used a tool called PiBakery which makes it a breeze to quickly create needed images with certain configurations. You can take a look at one of [my articles describing it&#8217;s usage](https://codeandunicorns.com/pibakery-example-first-setup-wifi-boot-vnc/) or at their [official website here.](http://www.pibakery.org/)

Screen resolution: Configuration change needed for Raspbian to fit this particular screen. Go into terminal and enter following command:

`nano /boot/config.txt`

Change framebuffer\_width to 1024 and framebuffer\_height to 768. Also uncomment in case you have it commented out.  
I also had some issues with outputting to HDMI and would strongly recommend changing hdmi\_force\_hotplug value to 1 from 0.  
After that save and exit,restart raspberry pi and you should be able to output via HDMI.

## **Items I bought: **

1.) LCD LED controller from Ebay: <http://www.ebay.co.uk/itm/112217998323>

2.) Due to length of the cable being to short I was forced to buy a longer one. If you want to know exactly what kind of cable you need it&#8217;s: 25 inch LVDS Cable 30 Pin 1 ch 6-bit FIX-30P-D6 For LCD Controller to Display. The most important part of this spec is FIX-30P-D6 which describes the connector etc.

## **Item I am still waiting for (battery): **

3.) [High Quality 19V, 5V,12V,16V,30000MAH LiPo USB Batteries for Laptop](https://www.aliexpress.com/item/High-Quality-19V-5V-12V-16V-30000MAH-LiPo-USB-Batteries-for-Laptop-Mobile-phone-Power-Bank/32570079504.html)

&nbsp;

<div class="fusion-button-wrapper fusion-aligncenter">
  <a class="fusion-button button-flat fusion-button-round button-large button-default button-8" target="_self" href="https://codeandunicorns.com/acer-travelmate-4150-retrofitting-raspberry-pi-laptop-part-1-lcd-cleanup/"><span class="fusion-button-text">Check Part 1 here</span></a>
</div>