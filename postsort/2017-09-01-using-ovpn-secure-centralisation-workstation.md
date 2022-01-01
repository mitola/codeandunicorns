---
id: 2288
title: Using OVPN as secure centralisation to your workstation
date: 2017-09-01T22:31:16+00:00
author: Matjaz Trcek
layout: post
guid: https://codeandunicorns.com/?p=2288
permalink: /using-ovpn-secure-centralisation-workstation/
fusion_builder_status:
  - ""
avada_post_views_count:
  - "2251"
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
  - "6113222421"
image: /wp-content/uploads/2017/09/OVPN_Windows_remote_desktop.jpg
categories:
  - ALL
---
## Why?

Why did I choose OVPN for me in this case? In short, this are the reasons:

  * Server location in Germany and Sweden
  * DNScrypt support
  * Their infrastructure does not store logs, neither their Custom Debian system has any support for SATA or USB.
  * Swedish jurisdiction
  * P2P protocol support allowed
  * And static IP4 support for centralisation in my case
  * some other add-ons that you can check on their website but I don&#8217;t really care for ATM. (Link [HERE](https://www.ovpn.com/en/pricing))
  * 4 simultaneous devices

## Setup guide:

**IP4 workstation:**

For your workstation download their Windows client (or Mac&#8217;s OVPN client of course) <https://www.ovpn.com/en/guides/windows>. Very simple setup, just use the OVPN credentials, with no extra certificates etc. required.

**iPhone:**

For iPhone you need to install OpenVPN Connect from the app store and send yourself a configuration file, which you&#8217;ll be able to download on <https://www.ovpn.com/en/guides/ios>. Just be careful to select the one with IP4 and your specific server or pool.

After you open file on your iPhone, beetwen the sharing options choose Copy to OpenVPN.

## Remote desktop

For remote desktop I prefer to use Windows Remote Desktop. They have clients for lots of systems from iOS to OS X to Windows to Android. They are fairly up to date, with all bells and whistles you could wish for in your remote access clients. There are a lot alternatives out there so try whatever your heart desires. But for me the ease of use, and Microsoft&#8217;s recent years return to glory in some software is a big plus for me, at least in this case.

URL for more info: <https://support.microsoft.com/en-us/help/17463/windows-7-connect-to-another-computer-remote-desktop-connection>

&nbsp;

**P.S.:**

My experience in using this 2 combinations is that it works like a charm. The only thing to be careful a bit off is to only use IPv4 module from OVPN only on the computer which you wish to dedicate as the workstation.

&nbsp;

&nbsp;

&nbsp;