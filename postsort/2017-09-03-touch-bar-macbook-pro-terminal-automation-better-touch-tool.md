---
id: 2275
title: 'Touch bar (Macbook pro) terminal automation &#8211; Better Touch Tool'
date: 2017-09-03T22:15:38+00:00
author: Matjaz Trcek
layout: post
guid: https://codeandunicorns.com/?p=2275
permalink: /touch-bar-macbook-pro-terminal-automation-better-touch-tool/
fusion_builder_status:
  - ""
avada_post_views_count:
  - "6167"
dsq_thread_id:
  - "6117456940"
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
image: /wp-content/uploads/2017/08/overview_better_touch_tool-min.png
categories:
  - ALL
---
Recently I upgraded my work computer to MacBook Pro 13 &#8221; with the new touch bar. But to be totally honest I quite dislike the default customisability of the touch bar that is included in os X by default.

After a careful and in depth review of different solutions that could be use to amend that situation I stumbled upon BetterTouchTool (BTT in short), which is a great productivity enchanter in many areas such as hotkeys, gestures etc.

But personally, I am at least for the time being only interested in their TouchBar capabilities. On the picture above it&#8217;s an example snapshot of couple of my current shortcuts/workflows. You can add buttons with images, just text or both. Or widgets as well such as for example a Spotify widget that nicely enhances the experience.

On the left side you can see several ways of touch bar config. For example Global ones will persist and application specific will only popup on the bar based on the application that you have opened. In my case for IntelliJ IDEA I use debug workflow to start up the lovely debugger.

But let&#8217;s cut the chase and take a look at a specific use case.

&nbsp;

<img class="aligncenter wp-image-2278 size-full" src="https://codeandunicorns.com/wp-content/uploads/2017/08/HippoCms_shortcut-min.png" alt="" width="1004" height="416" srcset="https://codeandunicorns.com/wp-content/uploads/2017/08/HippoCms_shortcut-min-200x83.png 200w, https://codeandunicorns.com/wp-content/uploads/2017/08/HippoCms_shortcut-min-300x124.png 300w, https://codeandunicorns.com/wp-content/uploads/2017/08/HippoCms_shortcut-min-400x166.png 400w, https://codeandunicorns.com/wp-content/uploads/2017/08/HippoCms_shortcut-min-600x249.png 600w, https://codeandunicorns.com/wp-content/uploads/2017/08/HippoCms_shortcut-min-768x318.png 768w, https://codeandunicorns.com/wp-content/uploads/2017/08/HippoCms_shortcut-min-800x331.png 800w, https://codeandunicorns.com/wp-content/uploads/2017/08/HippoCms_shortcut-min.png 1004w" sizes="(max-width: 1004px) 100vw, 1004px" /> 

[Hippo CMS](https://www.onehippo.com/en) (Bloomreach experience now) is a Java based CMS System in short. and since I thought oh why not make the launching a bit simpler? So I created a relatively simple workflow with couple of steps to connect to Terminal app first.

After that as you can see in the image below I attached keyboard shortcut to go to a right tab in the Terminal application. I always have when working with this particular system, the process itself opened in first tab, therefore the shortcut will always take me from the outer most right tab which due to how i am used to terminal is always opened (if theres more than one)  to move back to the first tab.

<img class="aligncenter wp-image-2280" src="https://codeandunicorns.com/wp-content/uploads/2017/08/Sending_shortcut_to_terminal-min.png" alt="" width="600" height="168" srcset="https://codeandunicorns.com/wp-content/uploads/2017/08/Sending_shortcut_to_terminal-min-200x56.png 200w, https://codeandunicorns.com/wp-content/uploads/2017/08/Sending_shortcut_to_terminal-min-300x84.png 300w, https://codeandunicorns.com/wp-content/uploads/2017/08/Sending_shortcut_to_terminal-min-400x112.png 400w, https://codeandunicorns.com/wp-content/uploads/2017/08/Sending_shortcut_to_terminal-min-600x168.png 600w, https://codeandunicorns.com/wp-content/uploads/2017/08/Sending_shortcut_to_terminal-min-768x214.png 768w, https://codeandunicorns.com/wp-content/uploads/2017/08/Sending_shortcut_to_terminal-min-800x223.png 800w, https://codeandunicorns.com/wp-content/uploads/2017/08/Sending_shortcut_to_terminal-min.png 1010w" sizes="(max-width: 600px) 100vw, 600px" /> 

Great, now we focused on correct tab, after that we stop running process of Hippo in case it still runs from before with a simple CTRL + C shortcut.

After that we input the text through typing (one of the options under Predefined Action) to make the rebuild. Command itself looks something like this:

`cd PATH_TO_PROJECT && mvn clean verify && mvn -P cargo.run`

Lovely, everything looks nice, we send ENTER button and it triggers a nice maven clean and build itself.

<p style="text-align: center;">
  <em>A small bit of automation to save seconds at a time, one by one. </em>
</p>