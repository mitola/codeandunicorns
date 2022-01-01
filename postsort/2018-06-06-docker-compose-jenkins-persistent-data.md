---
title: docker-compose Jenkins with persistent data
date: 2018-06-06T15:46:03+00:00
author: Matjaz Trcek
layout: post
guid: https://codeandunicorns.com/?p=2412
permalink: /docker-compose-jenkins-persistent-data/
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
  - "10310"
sbg_selected_sidebar:
  - 'a:1:{i:0;s:1:"0";}'
sbg_selected_sidebar_replacement:
  - 'a:1:{i:0;s:12:"Blog Sidebar";}'
sbg_selected_sidebar_2:
  - 'a:1:{i:0;s:1:"0";}'
sbg_selected_sidebar_2_replacement:
  - 'a:1:{i:0;s:0:"";}'
dsq_thread_id:
  - "6715257527"
image: /wp-content/uploads/2018/06/Screen-Shot-2018-06-06-at-3.27.25-PM.png
categories:
  - ALL
  - How to
  - The Code
---
This guide will focus on the local environment for now, but should be easy to adapt to higher env&#8217;s. The focus of the guide is how to run Jenkins image, add changes to it, and load then on next start.

Create a following file on your local machine and go to that location in the terminal.

docker-compose.yaml file:

<pre class="brush: bash; title: ; notranslate" title="">version: '2'
services:
  jenkins:
    image: 'jenkins/jenkins:lts'
    labels:
      kompose.service.type: nodeport
    ports:
      - '80:8080'
      - '443:8443'
      - '50000:50000'
    volumes:
      - 'jenkins_data:/jenkins_config'
volumes:
  jenkins_data:
    driver: local
</pre>

Under services: we define which image is used. I used the one from Docker hub located <https://hub.docker.com/r/jenkins/jenkins/>. Under tags you choose your own version but I prefer running on LTS at least while testing locally.

Kompose.service.type is used so it is also kompose compatible.

The volume is perhaps the most relevant in this case since we define the name & location of the volume hard as jenkins\_data:/jenkins\_config as well as defining type of driver used for volume.

&nbsp;

Cool, we have a nice yaml setup. Now in the terminal we execute  
`docker compose up`  
to fire up with the correct image etc. Now the actual jenkins should be available.

To check for your password that you will need for the first time check first which container id is associated with your newly ran container.

You can do that with:

`docker ps`

To actually check the logs use:

`docker logs CONTAINER_ID`

In the output of the above command you should see message like

`<br />
*************************************************************</p>
<p>Jenkins initial setup is required. An admin user has been created and a password generated.<br />
Please use the following password to proceed to installation:`

After going to the local Jenkins URL, setting up plugins etc. you can use  
`docker-compose stop` to persist data on the data volume.  
And upon next start simply use `docker-compose start` for it.

This is hopefully an easy and straightforward setup for anyone wanting to focus a bit more on CI/CD specific case.