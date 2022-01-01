---
id: 2110
title: Installing Docker on Linode with WordPress image
date: 2017-02-17T16:39:03+00:00
author: Matjaz Trcek
layout: post
guid: https://codeandunicorns.com/?p=2110
permalink: /installing-docker-on-linode-with-wordpress-image/
slide_template:
  - default
fusion_builder_status:
  - ""
avada_post_views_count:
  - "2940"
dsq_thread_id:
  - "5560451404"
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
image: /wp-content/uploads/2017/02/docker-wordpress.png
categories:
  - ALL
  - How to
  - The Code
---
After creating your new Debian/Ubuntu instance on your Linode manager console follow following steps.

**  
Instance update and docker install  
** 

1.) To upgrade your Linux instance with the newest relevant updates, to get our instance up to date (in our case running Ubuntu) .

`<br />
apt-get upgrade<br />
apt-get update<br />
` 

2.) There is an issue with Linode and Docker with dependancies, therefore following command needs to be run as well before continuing with docker installation:  
`<br />
apt-get install dmsetup && dmsetup mknodes<br />
` 

**Docker installation**

3.) After that we need to install Docker itself with a lovely curl command:  
`<br />
curl -sSL https://get.docker.com/ | sh<br />
` 

With that installation of Docker on Linode is finished. But it a very basic one.

Before getting WordPress image installed, image presumes you already have MySQL server running.

With this command we are creating docker image with wordpressdb name and adding password with mysql database name, as well as it&#8217;s version. In the following command we will use mysql:tag, with tag representing version 5.7.  
`<br />
docker run --name wordpressdb -e MYSQL_ROOT_PASSWORD=password -d mysql:5.7<br />
` 

Now we need to create WordPress image with the existing mysql container which we named in previous command, wordpressdb:  
`<br />
docker run --name wordpresscu --link wordpressdb:mysql -d wordpress<br />
` 

**Extra information:**

But since I was encountering problems with some part it&#8217;s important that if anyone needs it, that we add a command for removal of a container and showing all containers.

Displays all containers if they are run or not:  
`docker ps -a`

Removes the chosen container:  
`docker rm`