---
id: 2136
title: Duplicity scp/ssh backup on raspberry Pi
date: 2017-03-01T15:19:14+00:00
author: Matjaz Trcek
layout: post
guid: https://codeandunicorns.com/?p=2136
permalink: /duplicity-scpssh-backup-raspberry-pi/
slide_template:
  - default
fusion_builder_status:
  - ""
avada_post_views_count:
  - "4954"
dsq_thread_id:
  - "5594435753"
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
image: /wp-content/uploads/2017/02/Screen-Shot-2017-02-26-at-15.13.22-min.png
categories:
  - ALL
  - How to
  - The Code
---
[wp\_ad\_camp_1]  
I want to use duplicity to backup my cloud server on Linode (You can use AWS as well or any other provider through which you can scp/ssh). Why I want to use duplicity is also because or partial backups, since the first backup will be full and all continuous ones will be only for the difference in files.

Why Raspberry pi? It&#8217;s cheap, low power and very portable :)d

So let&#8217;s proceed with the setup.

### Prerequisites:

  * gpg
  * duplicity
  * ssh keys

### Installation and configuration:

Before anythign else, it is highly recomended your Raspberry Pi is up to date and that you run:  
`sudo apt-get update`

For installation of duplicity, after the update, it should run fairly smoothly with the following command:  
`sudo apt-get install duplicity`

In case you want encryption which I highly recommend, setting up GPG keys is recommended and supported by Duplicity. For that we first need to install GPG with:  
`sudo apt-get install gnupg`

Perfect, now we have the proper tool installed and need to generate appropriate key with all the info you will be required in the command prompt. Run this command and follow the instructions, and most importantly note them down somewhere! You don&#8217;t want to lose your password.

`gpg --gen-key`

At one point you will encounter &#8220;Not enough random bytes available. Please do some other work to give  
the OS a chance to collect more entropy!&#8221;  
And i simply didn&#8217;t have enough entropy.  
But if you want to know how big your entropy is you can check with cating:

`cat /proc/sys/kernel/random/entropy_avail`

For me it was 34. After that I have installed:

`sudo apt-get install rng-tools`

And it increased to over 1000. which is absolutely great. After that the GPG key got automatically generated. Do however note, that you need to run this entropy related commands in parallel to your terminal in another window.

When running `gpg –list-key` you should be able to see now your newly created gpg key.

Then let&#8217;s try it with:  
`duplicity full ssh:root:password@IPofHOST// home/pi/backup`  
This will fail. I just wished to demonstrate this so other people don&#8217;t need to investigate through the same problem, that is that duplicity can&#8217;t use remote as source.

As a solution I am mounting remote to be a fake local mount with:  
[`apt-get install sshfs`](http://serverfault.com/questions/543039/backup-a-remote-directory-with-duplicity)

After that we will run:  
`<br />
mkdir -p /mnt/remote &&<br />
sshfs root:password@IPofHOST:/ /mnt/remote<br />
` 

This will mount it locally and you can therefore specify your local backup paths for Duplicity

The mentioned tool has a range of commands, but one of them that you could potentially use for that would be then:

`duplicity /home/directory file://some/other/directory`

**Reference:**  
<http://go2linux.garron.me/scp-duplicity-secure-backup/>