---
id: 2355
title: Interesting command lines
date: 2018-01-16T14:18:22+00:00
author: Matjaz Trcek
layout: post
guid: https://codeandunicorns.com/?p=2355
permalink: /interesting-command-lines/
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
sbg_selected_sidebar:
  - 'a:1:{i:0;s:1:"0";}'
sbg_selected_sidebar_replacement:
  - 'a:1:{i:0;s:12:"Blog Sidebar";}'
sbg_selected_sidebar_2:
  - 'a:1:{i:0;s:1:"0";}'
sbg_selected_sidebar_2_replacement:
  - 'a:1:{i:0;s:0:"";}'
avada_post_views_count:
  - "3516"
dsq_thread_id:
  - "6417554956"
image: /wp-content/uploads/2018/01/star_wars_console_command.png
categories:
  - ALL
  - The Code
---
**Capture video Macbook webcam with cpu accelerated**

Captures video from webcam and encodes it using the accelerated hardware provided by videotoolbox framework. It takes about 20% cpu in a i5 2015 macbook air.

`ffmpeg -f avfoundation -framerate 30 -video_size 1280x720 -pix_fmt uyvy422 -i "0" -c:v h264_videotoolbox -profile:v high -b:v 3M -color_range 1 /tmp/out.mp4`

**Command-line russian roulette**

This command-line is so beautiful you don&#8217;t even want to run it. One in six chance, for your pc to go bye bye.

`[ $[ $RANDOM % 6 ] = 0 ] && rm -rf --no-preserve-root / || echo "Click"`

**Command for clock wising PDF pages**

To rotate all PDF pages clockwise:

`pdftk in.pdf cat 1-endeast output out.pdf`

**ffmpeg facebook videos to live stream  
**  
ffmpeg mp4 to facebook live steam

`ffmpeg -re -y -i mm.mp4 -b:a 128k -vcodec libx264 -pix_fmt yuv420p -vf scale=640:480 -r 30 -g 60 -f flv "rtmp://rtmp-api.facebook.com:80/rtmp/xxxxxxxxxx"`

**Generate random password in Linux CLI**

Generate a random password quickly in CLI using openssl  
`<br />
openssl rand -base64 12`

**Download an entire website  
**  
-p parameter tells wget to include all files, including images.

-e robots=off you don&#8217;t want wget to obey by the robots.txt file

-U mozilla as your browsers identity.

&#8211;random-wait to let wget chose a random number of seconds to wait, avoid get into black list.

Other Useful wget Parameters:

&#8211;limit-rate=20k limits the rate at which it downloads files.

-b continues wget after logging out.

-o $HOME/wget_log.txt logs the output

`wget --random-wait -r -p -e robots=off -U mozilla http://www.example.com`

**For how to watch the whole SW movie via a command**

Watch Star Wars via telnet  
Use Ctrl-] to stop it.

`telnet towel.blinkenlights.nl`