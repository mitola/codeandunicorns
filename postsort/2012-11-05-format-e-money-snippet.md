---
id: 100
title: Format € money snippet
date: 2012-11-05T13:01:04+00:00
author: Matjaz Trcek
layout: post
guid: http://codeandunicorns.com/?p=100
permalink: /format-e-money-snippet/
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
  - "2392"
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
categories:
  - The Code
tags:
  - format
  - function
  - javascript
  - JS
  - method
  - snippet
---
The following function transforms the inputed numeric value for example  
var sum = 50.3  
sum.formatMoney(2,&#8217;,&#8217; , &#8216;.&#8217;) + &#8220;€&#8221;  
and the output of this function is then 50,30€. As you notice it is quite simple to change it in $ or anything you desire.

<pre class="brush: jscript; title: ; notranslate" title="">Number.prototype.formatMoney = function(c, d, t){
    var n = this, c = isNaN(c = Math.abs(c)) ? 2 : c, d = d == undefined ? "," : d, t = t == undefined ? "." : t, s = n &lt; 0 ? "-" : "", i = parseInt(n = Math.abs(+n || 0).toFixed(c)) + "", j = (j = i.length) &gt; 3 ? j % 3 : 0;
    return s + (j ? i.substr(0, j) + t : "") + i.substr(j).replace(/(\d{3})(?=\d)/g, "$1" + t) + (c ? d + Math.abs(n - i).toFixed(c).slice(2) : "");
};

</pre>