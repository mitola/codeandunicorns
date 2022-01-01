---
id: 1098
title: File retrieval and changing img element with Bootstrap
date: 2015-04-24T09:40:05+00:00
author: Matjaz Trcek
layout: post
guid: http://codeandunicorns.com/?p=1098
permalink: /file-retrieval-and-changing-img-element-with-bootstrap/
slide_template:
  - default
pyre_full_width:
  - 'no'
pyre_transparent_header:
  - default
avada_post_views_count:
  - "2341"
fusion_builder_content_backup:
  - |
    Sharing a smaller code snippet / mini tutorial / example since I have found it very useful in connection to HTML preview display of cam image or an uploaded image, depending on what you want really :)
    So, the example is using Twitters Bootstrap, jQuery and beloved base64. I know the last one is just an encoding, but I like it nonetheless!
    
    In the following code a simple example is provided with an image which will be replaced later with uploaded image without reloading.
    
    [code lang="html"]
    
    &lt;!DOCTYPE html&gt;
    &lt;html lang=&quot;en&quot;&gt;
    &lt;head&gt;
    &lt;meta charset=&quot;utf-8&quot;&gt;
    &lt;meta http-equiv=&quot;X-UA-Compatible&quot; content=&quot;IE=edge&quot;&gt;
    &lt;meta name=&quot;viewport&quot; content=&quot;width=device-width, initial-scale=1&quot;&gt;
    
    &lt;title&gt;demo canvas example&lt;/title&gt;
    
    &lt;!-- Bootstrap Definitions --&gt;
    &lt;link href=&quot;css/bootstrap.min.css&quot; rel=&quot;stylesheet&quot;&gt;
    &lt;!-- Choosen font --&gt;
    &lt;link href='http://fonts.googleapis.com/css?family=Francois+One' rel='stylesheet' type='text/css'&gt;
    
    &lt;/head&gt;
    &lt;body&gt;
    
    &lt;div class=&quot;row text-center&quot; id=&quot;pass&quot; style=&quot;padding-bottom: 20px;&quot;&gt;
    &lt;div class=&quot;col-sm-10&quot;&gt;&lt;h2&gt;Image placeholder&lt;/h2&gt;&lt;/div&gt;
    &lt;div class=&quot;col-sm-12 &quot;&gt;
    &lt;img id=&quot;imagePreview&quot; height=&quot;220&quot; width=&quot;355&quot; src=&quot;chosenImage.jpg&quot;
    class=&quot;img-responsive center-block&quot; alt=&quot;&quot;&gt;
    &lt;!-- regarding btn-file class check at the bottom for a neat solution of making design same as for other Bootstrap buttons --&gt;
    &lt;span class=&quot;btn btn-primary btn-file&quot;&gt;
    &lt;!-- File upload button and file chooser --&gt;
    Upload &lt;input type=&quot;file&quot; id=&quot;fileuploadform&quot;&gt;
    &lt;/span&gt;
    &lt;/div&gt;
    
    &lt;/div&gt;
    &lt;!-- Scripts loading --&gt;
    &lt;!-- jQuery (necessary for Bootstrap's JavaScript plugins) --&gt;
    &lt;script src=&quot;https://ajax.googleapis.com/ajax/libs/jquery/1.11.2/jquery.min.js&quot;&gt;&lt;/script&gt;
    &lt;!-- Include all compiled plugins (below), or include individual files as needed --&gt;
    &lt;script src=&quot;js/bootstrap.min.js&quot;&gt;&lt;/script&gt;
    
    &lt;!-- This script can be seen in the next code section --&gt;
    &lt;script&gt;
    .... JS script part
    &lt;/script&gt;
    &lt;/body&gt;
    &lt;/html&gt;
    
    [/code]
    
    Javascript nicely separated :)
    
    [code lang="js"]
    var trimmedReaderResult;
    
    //If upload form is used, the following function will get triggered
    $(&quot;#fileuploadform&quot;).on('change', function () {
    previewAndSendDoc(1);
    })
    
    //following the workflow
    function previewAndSendDoc(whichDiv) {
    if (whichDiv === 1) {
    var uploadformid = 'fileuploadform';
    //Getting image named imagePreview, this &lt;img&gt; element will be used for manipulation
    var previewImg = document.getElementById('imagePreview');
    }
    //getting the file from the file upload button
    var uploadform = document.getElementById(uploadformid).files[0];
    //Initializing FileReader
    var reader = new FileReader();
    [/code]
    
    In this function reader function callback will be called after it finishes the file and replace image of <img alt="" /> previewImage element newly received file. After that in this case the base64 of the image will be taken and truncated until only binary data without prefix remains for further manipulation
    
    [code lang="js"]
    reader.onloadend = function () {
    previewImg.src = reader.result;
    trimmedReaderResult = reader.result.substring(reader.result.indexOf(',')+1);
    //getting pure base64 of image
    }[/code]
    
    Function which will go to the above function after readAsDataUrl is finished
    
    [code lang="js"]
    if (uploadform) {
    reader.readAsDataURL(uploadform);
    } else {
    previewImg.src = &quot;&quot;;
    }
    
    //sendingDocument();
    }[/code]
    
    And addition for colouring button for a file upload to have the same design as other Boostrap buttons:
    
    [code lang="css"]
    .btn-file {
    position: relative;
    overflow: hidden;
    }
    .btn-file input[type=file] {
    position: absolute;
    top: 0;
    right: 0;
    min-width: 100%;
    min-height: 100%;
    font-size: 100px;
    text-align: right;
    filter: alpha(opacity=0);
    opacity: 0;
    outline: none;
    background: white;
    cursor: inherit;
    display: block;
    }[/code]
    
fusion_builder_converted:
  - 'yes'
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
categories:
  - ALL
---
Sharing a smaller code snippet / mini tutorial / example since I have found it very useful in connection to HTML preview display of cam image or an uploaded image, depending on what you want really 🙂  
So, the example is using Twitters Bootstrap, jQuery and beloved base64. I know the last one is just an encoding, but I like it nonetheless!

In the following code a simple example is provided with an image which will be replaced later with uploaded image without reloading.

<div  class="fusion-fullwidth fullwidth-box hundred-percent-fullwidth"  style='background-color: #ffffff;background-position: center center;background-repeat: no-repeat;padding-top:0px;padding-right:0px;padding-bottom:0px;padding-left:0px;'>
  <div class="fusion-builder-row fusion-row ">
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: xml; title: ; notranslate" title="">

&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
&lt;head&gt;
&lt;meta charset="utf-8"&gt;
&lt;meta http-equiv="X-UA-Compatible" content="IE=edge"&gt;
&lt;meta name="viewport" content="width=device-width, initial-scale=1"&gt;

&lt;title&gt;demo canvas example&lt;/title&gt;

&lt;!-- Bootstrap Definitions --&gt;
&lt;link href="css/bootstrap.min.css" rel="stylesheet"&gt;
&lt;!-- Choosen font --&gt;
&lt;link href='http://fonts.googleapis.com/css?family=Francois+One' rel='stylesheet' type='text/css'&gt;

&lt;/head&gt;
&lt;body&gt;

&lt;div class="row text-center" id="pass" style="padding-bottom: 20px;"&gt;
&lt;div class="col-sm-10"&gt;&lt;h2&gt;Image placeholder&lt;/h2&gt;&lt;/div&gt;
&lt;div class="col-sm-12 "&gt;
&lt;img id="imagePreview" height="220" width="355" src="chosenImage.jpg"
class="img-responsive center-block" alt=""&gt;
&lt;!-- regarding btn-file class check at the bottom for a neat solution of making design same as for other Bootstrap buttons --&gt;
&lt;span class="btn btn-primary btn-file"&gt;
&lt;!-- File upload button and file chooser --&gt;
Upload &lt;input type="file" id="fileuploadform"&gt;
&lt;/span&gt;
&lt;/div&gt;

&lt;/div&gt;
&lt;!-- Scripts loading --&gt;
&lt;!-- jQuery (necessary for Bootstrap's JavaScript plugins) --&gt;
&lt;script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.2/jquery.min.js"&gt;&lt;/script&gt;
&lt;!-- Include all compiled plugins (below), or include individual files as needed --&gt;
&lt;script src="js/bootstrap.min.js"&gt;&lt;/script&gt;

&lt;!-- This script can be seen in the next code section --&gt;
&lt;script&gt;
.... JS script part
&lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;

</pre>
        
        <p>
          Javascript nicely separated 🙂
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: jscript; title: ; notranslate" title="">
var trimmedReaderResult;

//If upload form is used, the following function will get triggered
$("#fileuploadform").on('change', function () {
previewAndSendDoc(1);
})

//following the workflow
function previewAndSendDoc(whichDiv) {
if (whichDiv === 1) {
var uploadformid = 'fileuploadform';
//Getting image named imagePreview, this &lt;img&gt; element will be used for manipulation
var previewImg = document.getElementById('imagePreview');
}
//getting the file from the file upload button
var uploadform = document.getElementById(uploadformid).files[0];
//Initializing FileReader
var reader = new FileReader();
</pre>
        
        <p>
          In this function reader function callback will be called after it finishes the file and replace image of <img alt="" /> previewImage element newly received file. After that in this case the base64 of the image will be taken and truncated until only binary data without prefix remains for further manipulation
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: jscript; title: ; notranslate" title="">
reader.onloadend = function () {
previewImg.src = reader.result;
trimmedReaderResult = reader.result.substring(reader.result.indexOf(',')+1);
//getting pure base64 of image
}</pre>
        
        <p>
          Function which will go to the above function after readAsDataUrl is finished
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: jscript; title: ; notranslate" title="">
if (uploadform) {
reader.readAsDataURL(uploadform);
} else {
previewImg.src = "";
}

//sendingDocument();
}</pre>
        
        <p>
          And addition for colouring button for a file upload to have the same design as other Boostrap buttons:
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: css; title: ; notranslate" title="">
.btn-file {
    position: relative;
    overflow: hidden;
}
.btn-file input[type=file] {
    position: absolute;
    top: 0;
    right: 0;
    min-width: 100%;
    min-height: 100%;
    font-size: 100px;
    text-align: right;
    filter: alpha(opacity=0);
    opacity: 0;
    outline: none;
    background: white;
    cursor: inherit;
    display: block;
}</pre>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
  </div>
</div>