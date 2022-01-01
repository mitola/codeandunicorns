---
id: 206
title: 'Realistic human &#038; environment in Unity3d'
date: 2013-06-28T22:08:30+00:00
author: Matjaz Trcek
layout: post
guid: http://codeandunicorns.com/?p=206
permalink: /import-makehuman-human-into-unity3d/
image: /wp-content/uploads/2013/06/Unity3Dlogo.jpg
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
  - "6570"
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
    [youtube id="CrZJljDWzxU" width="600" height="350"]
    
    This is a short demo made relatively quickly with use of <a href="http://www.makehuman.org/">MakeHuman</a>, <a href="http://www.blender.org/">Blender</a> and <a href="http://unity3d.com/">Unity3d</a> .
    <h4>1.) MakeHuman object:</h4>
    First we created a "Human" which was aimed to be a jungle boy. For start simply open your MakeHuman program play with all the parameters and symetry etc. to get a desired effect. When you are happy with your model go under Files -&gt; Export -&gt; Collada and in export options you will also probably want to choose Eyelashes and Eyebrows options, use a decimeter size option and use either a simple rig or game rig, i personally prefer simple rig since i find it just enough complex and appropiate for my use. And it also includes all the necessary bones and spine for all the animation you'll need. After done with all your settings choose your file name and click export. When you are finished go to the Export folder in MakeHuman directory and you will see .dae format file with your model and folder "textures".
    <h4>2.) Painting cloth or skin:</h4>
    Go into folder "textures" and if you wish to make clothes, or different skin, you have multiple options. You can use Photoshop,Gimp,Paint(by using texture file) etc to paint the texture you get through export to make so called "clothes". Another option of making clothes is to use Blender and use paint texture tool on the body.
    <h4>3.) Importing in Unity3D and Animating:</h4>
    Ok, you have exported your object and colored it accordingly for import into Unity3d. Now it's time for interesting part. Choose your "Humanoid" assets and drag and drop them in the unity3d editor. Super, now you have a model. Drag and drop model from the project folder onto the scene and position it to your liking. You'll probably want to add some standard or extra animations in the new "Mekanim" . since it is best explained by video in my opinion in <a href="http://www.youtube.com/watch?v=Xx21y9eJq1U">THIS</a> youtube video is a link from unity on subject of <a href="http://www.youtube.com/watch?v=Xx21y9eJq1U">Mecanim Animation</a>. At least for me it was the fastest way to speedily learn the animation sequencing.  If you want to animate new moves i would suggest to take <a href="http://www.blender.org/education-help/tutorials/animation/">this</a> as a starting point, maybe it is not the best way, but i will update the post when i get more into this specific thematic.
    
    And when you import whole object in Unity3d , i'd suggest to use previous mentioned tutorial and their <a href="http://www.youtube.com/redirect?q=http%3A%2F%2Ffiles.unity3d.com%2Fwill%2FMecanimTute.zip&amp;session_token=YkxDrBKFNYtUO7qdaj9pYGZr_BV8MTM3MjU5NDU4N0AxMzcyNTA4MTg3">download</a> in the video description. And use their "Animations" folder to include into your project, so you have few animations to start with.
    <h4>4.) Making the terrain in unity3d</h4>
    That is one of the best features in Unity3D in my opinion. Just go under Terrain tab and choose "create Terrain" . After that, be the God, create your mountians, canyons, walls of unimaginable size, all what your heart desires.
    
    In the post i tried to represent one of possible pipelines for creating a game or at least as some kind of starting point for learning.
fusion_builder_converted:
  - 'yes'
categories:
  - ALL
  - Unity3D
tags:
  - 3d
  - Blender
  - Environment
  - Export
  - human
  - Import
  - MakeHuman
  - Terrain
  - Unity3D
---
<div  class="fusion-fullwidth fullwidth-box hundred-percent-fullwidth"  style='background-color: #ffffff;background-position: center center;background-repeat: no-repeat;padding-top:0px;padding-right:0px;padding-bottom:0px;padding-left:0px;'>
  <div class="fusion-builder-row fusion-row ">
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <div class="fusion-video fusion-youtube" style="max-width:600px;max-height:350px;">
          <div class="video-shortcode">
          </div>
        </div>
        
        <p>
          This is a short demo made relatively quickly with use of <a href="http://www.makehuman.org/">MakeHuman</a>, <a href="http://www.blender.org/">Blender</a> and <a href="http://unity3d.com/">Unity3d</a> .
        </p>
        
        <h4>
          1.) MakeHuman object:
        </h4>
        
        <p>
          First we created a &#8220;Human&#8221; which was aimed to be a jungle boy. For start simply open your MakeHuman program play with all the parameters and symetry etc. to get a desired effect. When you are happy with your model go under Files -> Export -> Collada and in export options you will also probably want to choose Eyelashes and Eyebrows options, use a decimeter size option and use either a simple rig or game rig, i personally prefer simple rig since i find it just enough complex and appropiate for my use. And it also includes all the necessary bones and spine for all the animation you&#8217;ll need. After done with all your settings choose your file name and click export. When you are finished go to the Export folder in MakeHuman directory and you will see .dae format file with your model and folder &#8220;textures&#8221;.
        </p>
        
        <h4>
          2.) Painting cloth or skin:
        </h4>
        
        <p>
          Go into folder &#8220;textures&#8221; and if you wish to make clothes, or different skin, you have multiple options. You can use Photoshop,Gimp,Paint(by using texture file) etc to paint the texture you get through export to make so called &#8220;clothes&#8221;. Another option of making clothes is to use Blender and use paint texture tool on the body.
        </p>
        
        <h4>
          3.) Importing in Unity3D and Animating:
        </h4>
        
        <p>
          Ok, you have exported your object and colored it accordingly for import into Unity3d. Now it&#8217;s time for interesting part. Choose your &#8220;Humanoid&#8221; assets and drag and drop them in the unity3d editor. Super, now you have a model. Drag and drop model from the project folder onto the scene and position it to your liking. You&#8217;ll probably want to add some standard or extra animations in the new &#8220;Mekanim&#8221; . since it is best explained by video in my opinion in <a href="http://www.youtube.com/watch?v=Xx21y9eJq1U">THIS</a> youtube video is a link from unity on subject of <a href="http://www.youtube.com/watch?v=Xx21y9eJq1U">Mecanim Animation</a>. At least for me it was the fastest way to speedily learn the animation sequencing.  If you want to animate new moves i would suggest to take <a href="http://www.blender.org/education-help/tutorials/animation/">this</a> as a starting point, maybe it is not the best way, but i will update the post when i get more into this specific thematic.
        </p>
        
        <p>
          And when you import whole object in Unity3d , i&#8217;d suggest to use previous mentioned tutorial and their <a href="http://www.youtube.com/redirect?q=http%3A%2F%2Ffiles.unity3d.com%2Fwill%2FMecanimTute.zip&session_token=YkxDrBKFNYtUO7qdaj9pYGZr_BV8MTM3MjU5NDU4N0AxMzcyNTA4MTg3">download</a> in the video description. And use their &#8220;Animations&#8221; folder to include into your project, so you have few animations to start with.
        </p>
        
        <h4>
          4.) Making the terrain in unity3d
        </h4>
        
        <p>
          That is one of the best features in Unity3D in my opinion. Just go under Terrain tab and choose &#8220;create Terrain&#8221; . After that, be the God, create your mountians, canyons, walls of unimaginable size, all what your heart desires.
        </p>
        
        <p>
          In the post i tried to represent one of possible pipelines for creating a game or at least as some kind of starting point for learning.
          
          <div class="fusion-clearfix">
          </div></div> </div></div></div>