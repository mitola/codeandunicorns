---
title: Finding faulty commit with git bisect
date: 2017-02-22T17:57:17+00:00
author: Matjaz Trcek
layout: post
guid: https://codeandunicorns.com/?p=2124
permalink: /finding-faulty-commit-with-git-bisect/
slide_template:
  - default
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
  - "2577"
dsq_thread_id:
  - "5575440454"
image: /wp-content/uploads/2017/02/382px-Binary_search_into_array_-_example.svg.png
categories:
  - How to
  - The Code
---
Recently the problem I have encountered was that the master got broken, possibly due to broken commit. Therefore I was investigating what would be the best and most appropriate way of finding a solution. Git bisect is a tool that uses binary search to find a faulty commit. Without something like this, your only other option is going through each of the commits until you found the one that is broken. In case where you look at a longer time frame, let&#8217;s say a week or a month, this method will help you to find it a lot faster then otherwise.

It works with first specifying one of the commits that contains the broken version and and one of the commits that works properly.

Here is an example:

`<br />
git bisect start<br />
git bisect bad # The version on which you are currently based with git you define as bad<br />
git bisect good f347fc667fb45dce4798f1d9469d44b696a790a2 # and this uses the commit that is working properly<br />
` 

This will checkout one of the random selected commits for a start probably somewhere in the middle. After you recompile your project and test it, you will see if it works or not.  
In case it works write:  
`<br />
git bisect good<br />
` 

If it doesn&#8217;t:  
`<br />
git bisect bad<br />
` 

Git bisect will return something like this:  
`Bisecting: 10 revisions left to test after this (roughly 4 steps)`

Continue with this step until you find the broken commit.  
After finding it and wishing to reset git bisect command use the following command to point it to head:  
`git bisect reset`

Good luck finding the naughty commits!

### References

Extra documentation and information on it, if needed:  
Official docs: <https://git-scm.com/docs/git-bisect>  
Blogger: <http://webchick.net/node/99>  
Stack overflow: <http://stackoverflow.com/questions/4713088/how-to-use-git-bisect>