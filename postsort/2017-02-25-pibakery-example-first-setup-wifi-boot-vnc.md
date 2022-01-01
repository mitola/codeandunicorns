---
title: Pibakery example of first setup with wifi and on boot VNC ( for updated version of pibakery)
date: 2017-02-25T13:48:07+00:00
author: Matjaz Trcek
layout: post
guid: https://codeandunicorns.com/?p=2130
permalink: /pibakery-example-first-setup-wifi-boot-vnc/
slide_template:
  - default
fusion_builder_status:
  - ""
avada_post_views_count:
  - "5837"
dsq_thread_id:
  - "5583387180"
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
image: /wp-content/uploads/2017/02/pibakery-example-min.png
categories:
  - ALL
  - Electronics
  - How to
---
Recently Pibakery has released an update with updated blocks, that changed quite a bit in comparison to previous versions and improved with several additions of the new building blocks or simplification of the previous ones. Now you even have cron job scheduler which is absolutely amazing!

### First boot:

Let&#8217;s start with taking a look at First boot part of the image above:

We start with enabling VLC at Boot. This is the only block i am not 100% if it needs to be done every time or only one time. But anyway, this will allow you to connect via your PC/OSx VLC client. I use a [VNC viewer ](https://www.realvnc.com/download/viewer/) for it, but there are many choices to choose from. When later on you connect your Raspberry pi to the network and find the IP, you should be able to connect to it by entering the ip with :0 or :5900 port at the end.

**Example:**

`192.1.0.245:0 or 192.1.0.245:5900`

The next option I have added is setting boot option block to a &#8220;Desktop logged in&#8221;, which will prove useful when using VNC, so you will be able to see the desktop without logging in or playing around the ssh.

After that I added another part of the recipe to the Pibakery template with setting the password of the future Rpi image, so you can make it at least more secure then having the default pi/raspberry combination.

After that I have added Wifi setup block with SSID and and password to automatically connect to it. And since I use Raspberry pi 3, it works beautifully out of the box.

&nbsp;

### On every boot:

As the last thing to the Pibakery I added VNC server at boot for now.

But in the future I would like to expand it with several additions, such as setting a cron job to automatically backup a remote server with duplicity.

&nbsp;