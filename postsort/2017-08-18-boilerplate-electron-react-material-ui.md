---
title: Boilerplate for Electron with React and Material UI
date: 2017-08-18T14:25:47+00:00
author: Matjaz Trcek
layout: post
guid: https://codeandunicorns.com/?p=2266
permalink: /boilerplate-electron-react-material-ui/
fusion_builder_status:
  - ""
avada_post_views_count:
  - "11032"
dsq_thread_id:
  - "6076134926"
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
image: /wp-content/uploads/2017/08/opengraph.png
categories:
  - ALL
---
I have created a boilerplate project for Electron used together in conjunction with React and Material UI, because too many projects in Javascript space have too many dependancies and it can be really hard for new developers to join this awesome community with so many options to explore!

You can check github repo for the Electron boilerplate at the end of the post.

The project itself uses Electron as basically only a wrapper for the actual functionality.

If we take a look at **src/App.js** file it gives a good point for where to continue.

<pre class="brush: jscript; title: ; notranslate" title="">const App = () =&gt; (
    &lt;div&gt;

    &lt;Grid container spacing={24}&gt;
        &lt;Grid item xs={6}&gt;
        &lt;LeftPanelComponent  /&gt;
        &lt;/Grid&gt;
        &lt;Grid item &gt;
        &lt;LeftPanelComponent  /&gt;
        &lt;/Grid&gt;
      &lt;/Grid&gt;
    &lt;/div&gt; 
);
</pre>

Inside the App we define Grid container with different items. The Grid container comes from (at the moment beta version) Material UI and acts in a very similar to Boostraps grid system.

Under: **src/components/LeftPanelComponent.js** there is an example of a component that gets connected into the grid in **App.js** .

The example component uses SimpleList component also originating from Material UI.

I know it may seem to be a bit short versed article, but I tried to make code as clear as possible.

Would love some feedback on potential improvements!

## References:

Github URL: <https://github.com/mitola/boilerplate-electron-material-ui-react>

Material UI: (Current beta docs docs) <https://material-ui-1dab0.firebaseapp.com/>

Material UI Icons: <https://www.npmjs.com/package/material-ui-icons>  
React tap event plugin: <https://github.com/zilverline/react-tap-event-plugin>  
Electron: <https://electron.atom.io/>