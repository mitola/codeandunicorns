---
id: 752
title: Simple .csv file parser
date: 2014-09-13T19:26:12+00:00
author: Matjaz Trcek
layout: post
guid: http://codeandunicorns.com/?p=752
permalink: /csv-file-multi-parser/
avada_post_views_count:
  - "2298"
slide_template:
  - default
pyre_video:
  - ""
pyre_full_width:
  - 'no'
pyre_sidebar_position:
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
pyre_fimg_width:
  - ""
pyre_fimg_height:
  - ""
pyre_image_rollover_icons:
  - linkzoom
pyre_link_icon_url:
  - ""
pyre_related_posts:
  - default
pyre_slider_position:
  - default
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
pyre_fallback:
  - ""
pyre_page_bg_layout:
  - default
pyre_page_bg:
  - ""
pyre_page_bg_color:
  - ""
pyre_page_bg_full:
  - 'no'
pyre_page_bg_repeat:
  - repeat
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
pyre_page_title:
  - default
pyre_page_title_text:
  - 'yes'
pyre_page_title_custom_text:
  - ""
pyre_page_title_custom_subheader:
  - ""
pyre_page_title_height:
  - ""
pyre_page_title_bar_bg:
  - ""
pyre_page_title_bar_bg_retina:
  - ""
pyre_page_title_bar_bg_full:
  - default
pyre_page_title_bar_bg_color:
  - ""
pyre_page_title_bg_parallax:
  - default
sbg_selected_sidebar:
  - 'a:1:{i:0;s:1:"0";}'
sbg_selected_sidebar_replacement:
  - 'a:1:{i:0;s:12:"Blog Sidebar";}'
fusion_builder_content_backup:
  - |
    In the following short snippet is an example of using PHP for simple parsing of .csv file / files comparing them and outputting the results in a third file. In this case itself it is not appropriate for use on live websites/apps since it is really inefficient, but I liked the simplicity and quick adaptability as a basis :) The snippet uses only functions and libs from PHP itself (5.2+)
    
    [code lang="php"]
    
    &lt;?php
    
    $all_acc_file = fopen('big_original_file.csv', 'r'); // test matchingdatacheck.csv
    $result_file = fopen(&quot;result.csv&quot;,&quot;w&quot;);
    
    $i = 0;
    $result_found=0;
    while (($line = fgetcsv($all_acc_file)) !== FALSE) {
    //$line is an array of the csv elements
      //print_r($line);
      $file_missmatch = fopen('comparison_table.csv', 'r');
      while (($linemiss = fgetcsv($file_missmatch)) !== FALSE) {
    
      //matching in this example twelth or seventh entry beetwen a line in big_original_file.csv and a line in comparison_table.csv
      if($line[11] == $linemiss[11] || $line[6] == $linemiss[6]){
        $result_arr = array($linemiss[2] , $linemiss[3] , $line[2] , $line[3],$line[11],$line[6]);
        $result_found=1;
       }
    }
    
    if($result_found==1){
      fputcsv($result_file, $result_arr);
    }
    
    fclose($file_missmatch);
    $i++; echo&quot;$in&quot;;
    $result_found=0;
    }
    
    fclose($all_acc_file);
    fclose($result_file);&lt;/pre&gt;
    [/code]
    
fusion_builder_converted:
  - 'yes'
categories:
  - ALL
tags:
  - csv
  - parser
  - PHP
---
In the following short snippet is an example of using PHP for simple parsing of .csv file / files comparing them and outputting the results in a third file. In this case itself it is not appropriate for use on live websites/apps since it is really inefficient, but I liked the simplicity and quick adaptability as a basis 🙂 The snippet uses only functions and libs from PHP itself (5.2+)

<div  class="fusion-fullwidth fullwidth-box hundred-percent-fullwidth"  style='background-color: #ffffff;background-position: center center;background-repeat: no-repeat;padding-top:0px;padding-right:0px;padding-bottom:0px;padding-left:0px;'>
  <div class="fusion-builder-row fusion-row ">
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: php; title: ; notranslate" title="">

&lt;?php

$all_acc_file = fopen('big_original_file.csv', 'r'); // test matchingdatacheck.csv
$result_file = fopen("result.csv","w");

$i = 0;
$result_found=0;
while (($line = fgetcsv($all_acc_file)) !== FALSE) {
   //$line is an array of the csv elements
   //print_r($line);
   $file_missmatch = fopen('comparison_table.csv', 'r');
   while (($linemiss = fgetcsv($file_missmatch)) !== FALSE) {

   //matching in this example twelth or seventh entry beetwen a line in big_original_file.csv and a line in comparison_table.csv
   if($line[11] == $linemiss[11] || $line[6] == $linemiss[6]){
     $result_arr = array($linemiss[2] , $linemiss[3] , $line[2] , $line[3],$line[11],$line[6]);
     $result_found=1;
   }
 }

 if($result_found==1){
   fputcsv($result_file, $result_arr);
 }

 fclose($file_missmatch);
 $i++; echo"$i\n";
 $result_found=0;
}

fclose($all_acc_file);
fclose($result_file);&lt;/pre&gt;
</pre>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
  </div>
</div>