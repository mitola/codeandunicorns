---
id: 84
title: Correct width in all browsers (JS snippet)
date: 2012-11-04T17:24:53+00:00
author: Matjaz Trcek
layout: post
guid: http://codeandunicorns.com/?p=84
permalink: /width-in-browser-js-snippet/
image:
  - ""
seo_follow:
  - 'false'
seo_noindex:
  - 'false'
pyre_page_title:
  - 'no'
pyre_page_title_text:
  - 'yes'
pyre_video:
  - ""
pyre_full_width:
  - 'no'
pyre_sidebar_position:
  - default
pyre_slider_type:
  - 'no'
pyre_slider:
  - "0"
pyre_wooslider:
  - "0"
pyre_flexslider:
  - "0"
pyre_revslider:
  - "0"
pyre_elasticslider:
  - "0"
pyre_fallback:
  - ""
pyre_page_bg_color:
  - ""
pyre_page_bg:
  - ""
pyre_page_bg_full:
  - 'no'
pyre_page_bg_repeat:
  - repeat
pyre_page_title_bar_bg:
  - ""
pyre_page_title_bar_bg_retina:
  - ""
pyre_page_title_bar_bg_color:
  - ""
pyre_fimg_width:
  - ""
pyre_fimg_height:
  - ""
pyre_image_rollover_icons:
  - linkzoom
pyre_link_icon_url:
  - ""
pyre_related_posts:
  - 'yes'
avada_post_views_count:
  - "3136"
slide_template:
  - default
pyre_display_header:
  - 'yes'
pyre_transparent_header:
  - default
pyre_displayed_menu:
  - default
pyre_display_footer:
  - default
pyre_display_copyright:
  - default
pyre_slider_position:
  - default
pyre_page_bg_layout:
  - default
pyre_wide_page_bg:
  - ""
pyre_wide_page_bg_color:
  - ""
pyre_wide_page_bg_full:
  - 'no'
pyre_wide_page_bg_repeat:
  - repeat
pyre_header_bg:
  - ""
pyre_header_bg_color:
  - ""
pyre_header_bg_full:
  - 'no'
pyre_header_bg_repeat:
  - repeat
pyre_page_title_custom_text:
  - ""
pyre_page_title_custom_subheader:
  - ""
pyre_page_title_height:
  - ""
pyre_page_title_bar_bg_full:
  - default
pyre_page_title_bg_parallax:
  - default
sbg_selected_sidebar:
  - 'a:1:{i:0;s:1:"0";}'
sbg_selected_sidebar_replacement:
  - 'a:1:{i:0;s:12:"Blog Sidebar";}'
fusion_builder_content_backup:
  - |
    This is a short JS snippet which is quite hard to find but it works like a charm.
    Basically with help of this JS snippet you get your width of the page correctly
    displayed in old IE6 and IE4 if you need to make it compatible with them or
    android/chrome/other browsers.
    
    [code lang="js"]
    function get_width() {
    var myWidth = 0;
    if(document.width) {
    //chrome
    myWidth = document.width;
    } else if( typeof( window.innerWidth ) == 'number' ) {
    //Non-IE
    myWidth = window.innerWidth;
    } else if( document.documentElement &amp;&amp; ( document.documentElement.clientWidth) ) {
    //IE 6+ in 'standards compliant mode'
    myWidth = document.documentElement.clientWidth;
    } else if( document.body &amp;&amp; ( document.body.clientWidth ) ) {
    //IE 4 compatible
    myWidth = document.body.clientWidth;
    }
    return myWidth;
    }
    [/code]
    
    And here is another JS snippet which does the same super compatibility except with height now width.
    
    [code lang="js"]
    function get_height() {
    var myHeight = 0;
    if(document.height) {
    //chrome
    myHeight = document.height;
    } else if( typeof( window.innerHeight ) == 'number' ) {
    //Non-IE
    myHeight = window.innerHeight;
    } else if(document.documentElement &amp;&amp; (document.documentElement.clientHeight)) {
    //IE 6+ in 'standards compliant mode'
    myHeight = document.documentElement.clientHeight;
    } else if(document.body &amp;&amp; (document.body.clientHeight)) {
    //IE 4 compatible
    myHeight = document.body.clientHeight;
    }
    return myHeight;
    }
    [/code]
    
    This JS snippets can be quite hard to find so hopefully this helps people who are searching for something like this.
fusion_builder_converted:
  - 'yes'
categories:
  - The Code
tags:
  - function
  - IE4
  - IE6
  - javascript
  - JS
---
This is a short JS snippet which is quite hard to find but it works like a charm.  
Basically with help of this JS snippet you get your width of the page correctly  
displayed in old IE6 and IE4 if you need to make it compatible with them or  
android/chrome/other browsers.

<div  class="fusion-fullwidth fullwidth-box hundred-percent-fullwidth"  style='background-color: #ffffff;background-position: center center;background-repeat: no-repeat;padding-top:0px;padding-right:0px;padding-bottom:0px;padding-left:0px;'>
  <div class="fusion-builder-row fusion-row ">
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: jscript; title: ; notranslate" title="">
function get_width() {
    var myWidth = 0;
    if(document.width) {
    //chrome
    myWidth = document.width;
    } else if( typeof( window.innerWidth ) == 'number' ) {
    //Non-IE
    myWidth = window.innerWidth;
    } else if( document.documentElement && ( document.documentElement.clientWidth) ) {
    //IE 6+ in 'standards compliant mode'
    myWidth = document.documentElement.clientWidth;
    } else if( document.body && ( document.body.clientWidth ) ) {
    //IE 4 compatible
    myWidth = document.body.clientWidth;
    }
    return myWidth;
 }
</pre>
        
        <p>
          And here is another JS snippet which does the same super compatibility except with height now width.
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: jscript; title: ; notranslate" title="">
function get_height() {
   var myHeight = 0;
   if(document.height) {
   //chrome
   myHeight = document.height;
   } else if( typeof( window.innerHeight ) == 'number' ) {
   //Non-IE
   myHeight = window.innerHeight;
   } else if(document.documentElement && (document.documentElement.clientHeight)) {
   //IE 6+ in 'standards compliant mode'
   myHeight = document.documentElement.clientHeight;
   } else if(document.body && (document.body.clientHeight)) {
   //IE 4 compatible
   myHeight = document.body.clientHeight;
   }
   return myHeight;
}
</pre>
        
        <p>
          This JS snippets can be quite hard to find so hopefully this helps people who are searching for something like this.
          
          <div class="fusion-clearfix">
          </div></div> </div></div></div>