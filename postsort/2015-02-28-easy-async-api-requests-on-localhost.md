---
id: 993
title: Easy async API requests on localhost
date: 2015-02-28T11:26:26+00:00
author: Joao Pereira
layout: post
guid: http://codeandunicorns.com/?p=993
permalink: /easy-async-api-requests-on-localhost/
slide_template:
  - default
pyre_full_width:
  - 'no'
pyre_transparent_header:
  - default
avada_post_views_count:
  - "2801"
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
  - linkzoom
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
  - 'no'
pyre_page_title_breadcrumbs_search_bar:
  - default
pyre_page_title_text:
  - 'yes'
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
image: /wp-content/uploads/2015/02/GoodNewsEveryone.jpg
categories:
  - How to
---
There comes a time for API developers when it’s handy to debug on localhost, the problem is that normally there are numerous asynchronous requests from third party API’s which can prove difficult to debug.

As an example, recently I was required to work on a custom payment system based on Woocommerce and PayPal’s Adaptive Payments, and I needed to check the PayPal’s IPN request hooked to Woocommerce on localhost. There are a number of ways to expose your localhost to the world but this method I’ll describe below is by far the easiest I have ever found which I believe can be handy for anyone in a similar situation.

### The tools

In order to expose your localhost we will be using a handy tool called localtunnel, it’s pretty straightforward to install if you’re Node.js developer, just follow the step provided in localtunnel’s website:

> npm install -g localtunnel

If you don’t have Node,js’ npm, then go ahead and install it. If you use Homebrew it’s as simple as:

> brew install node

### Making sure everything looks good

Just a quick check to see if everything is ok:

> node -v  
> npm -v

These should print the version on the console. Now we are set to start directing api calls with localtunnel:

> lt &#8211;port 80

Defining the port is important, be sure your web app is listening on the same port. After running the last command, localtunnel will provide you an exposed url like:

> https://xwttelmihf.localtunnel.me

You should now be able to access your web app through this url, so go ahead and open a browser to check it out. On my case I just double checked my httpd-vhosts.conf, confirmed my app was receiving traffic on port 80 and used localtunnel’s url when setting up the IPN Response URL like so:

> $args = array( &#8216;wc-api&#8217; => &#8216;WC_MyPayPalExampleAPI&#8217;,  
> &#8216;paypal\_chain\_ipn&#8217; => &#8216;1&#8217;,  
> &#8216;order\_id&#8217; => $order\_id,);  
> $payRequest->ipnNotificationUrl = add\_query\_arg( $args, &#8216;https://xwttelmihf.localtunnel.me/&#8217; ) ;

And there it is, you are now set in probably less than 10 minutes to start debugging your web hooks locally using localtunnel.

### Some $references if you need an extra hand:

#### 1 &#8211; [localtunnel step-by-step](https://localtunnel.me/)

#### 2 &#8211; [Official Github repo](https://github.com/defunctzombie/localtunnel)

#### 3 &#8211; [Node.js’ install guide](http://nodejs.org/download/)