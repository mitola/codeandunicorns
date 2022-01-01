---
id: 2534
title: How to start Go like a pro
date: 2018-11-14T15:48:47+00:00
author: Matjaz Trcek
layout: post
guid: https://codeandunicorns.com/?p=2534
permalink: /start-go-like-pro/
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
avada_post_views_count:
  - "2231"
sbg_selected_sidebar:
  - 'a:1:{i:0;s:1:"0";}'
sbg_selected_sidebar_replacement:
  - 'a:1:{i:0;s:12:"Blog Sidebar";}'
sbg_selected_sidebar_2:
  - 'a:1:{i:0;s:1:"0";}'
sbg_selected_sidebar_2_replacement:
  - 'a:1:{i:0;s:0:"";}'
image: /wp-content/uploads/2018/11/go-lang.png
categories:
  - How to
  - The Code
---
Presentation of my personal setup and suggestion for preparing a nice Go environment and some other resources in which you can feel comfortable to start bashing out the code.

Lets have a quick lookup:

  * [Visual Code](https://code.visualstudio.com) : 
      * On the Visual code install Go extension.
  * [Go](https://golang.org/dl/) (duh) 
      * But more importantly there are a nice of number tools that you would really want to run with Visual Code and Golang. Some of them are of course by default by some added later. They are (Of course check each tool separately if they apply to you): 
          * addr2line  
            asm  
            buildid  
            cgo  
            compile  
            cover  
            dist  
            doc  
            fix  
            link  
            nm  
            objdump  
            pack  
            pprof  
            test2json  
            tour  
            trace  
            vet
      * Didn&#8217;t really wish to go in depth on them since you can easily check them in more detail separately in a better source such as [Dominik&#8217;s list of Go tools](https://dominik.honnef.co/posts/2014/12/an_incomplete_list_of_go_tools/) or [Awesome go](https://awesome-go.com) where you can also find a lot more necessary and useful information.
  * Some of the resources that i found useful while picking up the language and getting up to speed with it: 
      * [Project based learning](https://github.com/tuvtran/project-based-learning#go)
      * [Hackr.io tutorials](https://hackr.io/tutorials/learn-golang) (Really nice collection of the resources)
      * [Gitbook](https://astaxie.gitbooks.io/build-web-application-with-golang/content/en/index.html) (with many examples)
      * [Go by Example](https://gobyexample.com) (Short but sweet)
  * It&#8217;s good to think about [tests](https://golang.org/pkg/testing/)
  * At some point you will really want to find an [easier way for struct-ing](https://transform.now.sh/json-to-go/) your JSON thingies

&nbsp;