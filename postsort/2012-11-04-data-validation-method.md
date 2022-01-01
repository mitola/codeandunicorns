---
id: 91
title: 3 Data validation methods in javascript
date: 2012-11-04T18:43:44+00:00
author: Matjaz Trcek
layout: post
guid: http://codeandunicorns.com/?p=91
permalink: /data-validation-method/
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
  - "2712"
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
  - function
  - javascript
  - method
---
Function is isValideDate can be used for example on a string data.isValideDate() to confirm that date is in correct format like these 2 for example:

  * 04-11-2012
  * 4-11-12

The isNumeric function is used same way with data.isNumeric() on a string and the function is used validation if the whole input is numeric

<pre class="brush: jscript; title: ; notranslate" title="">String.prototype.isValidDate = function()
{
    var IsoDateRe = new RegExp("^([0-9]{2})-([0-9]{2})-([0-9]{4})$");
    var matches = IsoDateRe.exec(this);
    if (!matches) return false;
    var composedDate = new Date(matches[3], (matches[2] - 1), matches[1]);
    return ((composedDate.getMonth() == (matches[2] - 1)) &&
        (composedDate.getDate() == matches[1]) &&
        (composedDate.getFullYear() == matches[3]));
}

String.prototype.isNumeric = function () {
    var intRegex = /^\d+$/;

    var v = this;

    if(intRegex.test(v)) {
        return true;
    }
    return false;
}
</pre>

And just for you, a third function for strings. This function data.isDouble() checks if the inputed data is of a double type.

<pre class="brush: jscript; title: ; notranslate" title="">String.prototype.isDouble = function () {
    var validChars = '0123456789.';

    for(var i = 0; i &lt; this.length; i++) {
        if(validChars.indexOf(this.charAt(i)) == -1)
            return false;
    }
    var dblVar = parseFloat(this);

    if(isNaN(dblVar))
        return false;
    return true;;
}
</pre>