---
id: 2439
title: Kubernetes Dashboard with kops
date: 2018-07-18T13:01:05+00:00
author: Matjaz Trcek
layout: post
guid: https://codeandunicorns.com/?p=2439
permalink: /kubernetes-dashboard-kops/
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
  - "5888"
dsq_thread_id:
  - "6800680972"
sbg_selected_sidebar:
  - 'a:1:{i:0;s:1:"0";}'
sbg_selected_sidebar_replacement:
  - 'a:1:{i:0;s:12:"Blog Sidebar";}'
sbg_selected_sidebar_2:
  - 'a:1:{i:0;s:1:"0";}'
sbg_selected_sidebar_2_replacement:
  - 'a:1:{i:0;s:0:"";}'
image: /wp-content/uploads/2018/07/kops_kube_dashboard.png
categories:
  - ALL
  - The Code
tags:
  - kops
  - kubernetes
  - terraform
---
Following is an example of simplest possible setup of dashboard add-on for kops. By default we utilize the official yaml configuration which already works fabulously with basic user-authentication. That should be perfect for a very small or one person team. Generally though, it is very smart to double check security of the monitoring service itself and extend upon it.

  1. First run the yaml configuration of kops dashboard add-on:  
    `<code>kubectl create -f <a href="https://raw.githubusercontent.com/kubernetes/kops/master/addons/kubernetes-dashboard/v1.8.3.yaml">https://raw.githubusercontent.com/kubernetes/kops/master/addons/kubernetes-dashboard/v1.8.3.yaml</a>`</code>&nbsp;
  2. Go to URL that got created:To get the URL:`<br />
kubectl cluster-info | grep master<br />
`  
    Example URL:`<code><br />
https://api-yoururl.amazonaws.com/ui`</code>&nbsp;
  3. To get the login token that you will be asked on the URL:  
    `<code>kubectl get secret $(kubectl get serviceaccount dashboard -o jsonpath="{.secrets[0].name}") -o jsonpath="{.data.token}" | base64 --decode`</code>&nbsp;
  4. Default login credentials you can get by using following kops command in terminal:  
    Username: admin  
    Password: (using command)`<code>kops get secrets kube --type secret -oplaintext`</code>&nbsp;
  5. But for now majority of the panels will be not viewable or available for edit etc. To fix this we will create a service account with access to default namespace and do a clusterrolebinding. However for future, it is good to have as much things as possible on NOT default namespace. <pre class="brush: bash; title: ; notranslate" title="">#To create a service account with access to default namespace
kubectl create serviceaccount dashboard -n default
 
 
#To create a cluster role bind. Connecting service account and cluster level access
kubectl create clusterrolebinding dashboard-admin -n default \
--clusterrole=cluster-admin \
--serviceaccount=default:dashboard </pre>