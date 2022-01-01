---
id: 1275
title: Nodebox 3 how to tutorial
date: 2015-07-27T16:49:32+00:00
author: Matjaz Trcek
layout: post
guid: https://codeandunicorns.com/?p=1275
permalink: /nodebox-3-how-to-tutorial/
slide_template:
  - default
pyre_full_width:
  - 'no'
pyre_transparent_header:
  - default
avada_post_views_count:
  - "5309"
dsq_thread_id:
  - ""
fusion_builder_status:
  - inactive
fusion_builder_content_backup:
  - |
    <strong>What: </strong>
    
    NodeBox is a node-based software application for generative design. It helps designers and everyone that uses it to automate boring productiong challenges, visualise large sets of data and manipulate the raw power of computer without using mechanical language of machines. The tools are able to integrate with traditional design applications and are cross platform.
    
    In my case it was used as a tool for artistic expression and beauty of the heart.
    
    &nbsp;
    
    <strong>Where:</strong>
    
    Main page: <a href="https://www.nodebox.net/node/">https://www.nodebox.net/node/</a>
    
    Download: <a href="https://www.nodebox.net/download/">https://www.nodebox.net/download/</a>
    
    <strong>The project:</strong>
    
    Explanation of the project itself. followed by through explanation of tutorial with pictures etc explanation of workflows and rendering. It is at least in a nice part based on howtos of <a href="https://www.nodebox.net/node/documentation/tutorial/getting-started.html" target="_blank">Nodebox wikis and tutorial</a>, with some changes to make it more suit to my purpose as for example retracing animations and shapes  by letter shapes, reconfiguring the borders  a few different things on color algorithms, but don't worry. We will cover most of the needed things in this tutorial.
    
    &nbsp;
    
    Before we go too into depth I will first try to explain the following graphical representation and a bit about Nodebox 3 specifically at the same time. So, the software itself is meant to be used as a tool toward generative design, mathematical and data representation in a visual way. In this case I had used it as a tool of artistic expression, or at least so I have envisioned my use. Also you can do everything through programming and only Nodebox version 3 enables you to do it in as intuitive and useful way like you can see here. They also offer library for Open GL which is bloody good. Maybe some fun and intriguing use can be found for games or virtual reality ?
    
    &nbsp;
    
    For this tutorial I will also assume basic knowledge and that you have done the official tutorial which is <strong>here</strong> and also part of the references and things that I find connected at the bottom of the article. And for this current variation of nodes, it may help taking the original tutorial and checking the differences or using the following images as better reference and maybe learning in process how to make it your own with some fluffy new funny variations. And <strong>now</strong> directly to the already done node diagram bellow.
    
    &nbsp;
    
    Overral description of the diagram:
    
    You get a number in a defined range from range1 node. Run that number through 3 separate nodes of add1 divide1 and multiply1. From there the new unique numbers continue down the path. One to the wave1 which will take care for wave generation and the wave1 output will be the input of make_point1. Which will actually visualize the dots based on the waveform itself. The divide node is used as a parameters for ellipse1, if i am correct it should be used for width and height.
    
    Ok now lets jump to the right side. Through the colour modes you provide your choice of colours (you can also use RGB nodes if you want instead). From there colour nodes are connected to the combine list and to repeat list. Which basically in practice means that the different make_points will be covered in a certain colour for certain length of points. For example 5 consecutive points...
    
    From the make_point lover we go to ellipse which just defines the shape of the points, following by colourize which will help us colour the points themselves, via a normal connection like on the picture of a group1 one followed by align1 node. copy1 node settings will be explained more in detail bellow on a separate picture. Via scale1 node you can define the sizes and scalation of your wavy points. If you are wondering what are those lines that go into left upper direction... they are parent inputs which a parent network of nodes provide to a child network group which is what we see at the moment.
    
    &nbsp;
    
    <a href="https://codeandunicorns.com/wp-content/uploads/2015/07/1.jpg"><img class="aligncenter size-full wp-image-1278" src="https://codeandunicorns.com/wp-content/uploads/2015/07/1.jpg" alt="1" width="810" height="695" /></a>
    
    &nbsp;
    
    On the middle top you have range node, which you use through its settings  and manipulate the range of the number generated. From there i sent the number in 3 ways, from addition node to dividing node and multiplying node.
    
    The addition node continues to wave1 form which other argument comes from a parent (Basically you can use grouping for a lot of modes, and use that group as a single node one level up the hierarchy and define which inputs are available from the upper hierarchy down etc. The grouping itself can be done via selection and right click until you see a menu to create a subnetwork). From wave1 node (where you can set up the wave size and repeat period through its parameters - picture screen can be seen below) which defines the size of a wave we continue to make_point1 which will create actual point themselves.
    
    &nbsp;
    
    <a href="https://codeandunicorns.com/wp-content/uploads/2015/07/2Capture.jpg"><img class="aligncenter size-full wp-image-1279" src="https://codeandunicorns.com/wp-content/uploads/2015/07/2Capture.jpg" alt="2Capture" width="769" height="416" /></a>
    
    &nbsp;
    
    Example of used wave1 node with current configuration of sizes period and type.
    
    <a href="https://codeandunicorns.com/wp-content/uploads/2015/07/3wave1.jpg"><img class="aligncenter size-full wp-image-1280" src="https://codeandunicorns.com/wp-content/uploads/2015/07/3wave1.jpg" alt="3wave1" width="332" height="239" /></a>
    
    &nbsp;
    
    Exact configuration of copy1 node. If you look closely you can see that I have chosen 9 copies with 40 angle rotation. Due to this node you can create a circley slightly angled starfish like looking structure. It basically takes the wave points created before which were also coloured, takes that makes 9 copies of them and angles everything together around a common centre point.
    
    <a href="https://codeandunicorns.com/wp-content/uploads/2015/07/4copy1.jpg"><img class="aligncenter size-full wp-image-1281" src="https://codeandunicorns.com/wp-content/uploads/2015/07/4copy1.jpg" alt="4copy1" width="436" height="275" /></a>
    
    &nbsp;
    
    Ok, the lowest level is finished for the time being. Select all the nodes, press right mouse button and choose Group into Network. and name it a thing. Connect 2 random_numbers nodes and a frame nod like you see on the picture. You can actually ignore the mod and add nodes since I have just forgot to remove them while doing this.
    
    This and the next picture are showing you confighs for random_numbers1 and random_numbers2 node configurations which I have chosen. After all is done feel free to play with any configs with keeping the eye on the changes.
    
    <img class="aligncenter size-full wp-image-1282" src="https://codeandunicorns.com/wp-content/uploads/2015/07/5randomnumbers1.jpg" alt="5randomnumbers1" width="903" height="953" />
    
    &nbsp;
    
    <a href="https://codeandunicorns.com/wp-content/uploads/2015/07/6randomnumbers2.jpg"><img class="aligncenter size-full wp-image-1283" src="https://codeandunicorns.com/wp-content/uploads/2015/07/6randomnumbers2.jpg" alt="6randomnumbers2" width="746" height="937" /></a>
    
    Showing the thing config which contains all the low level node configuration seen from earlier.
    
    <a href="https://codeandunicorns.com/wp-content/uploads/2015/07/7overallview.jpg"><img class="aligncenter size-large wp-image-1284" src="https://codeandunicorns.com/wp-content/uploads/2015/07/7overallview-1024x543.jpg" alt="7overallview" width="669" height="355" /></a>
    
    And now comes the proper fun part of the tutorial with awesome looks and all the glitter!
    
    Create nodes according to the image bellow.
    
    For the randomnumbers1 values are: 50 min and 500 max
    
    For the randomnumbers2 values are: 0 min and 800 max
    
    For the randomnumbers3 values are: 0.75 min and 4.00 max
    
    For the range1 start is 0.00 and Step property is 1.00.
    
    For the number1 itself I do actually think the number itself is not so important since I circumvented it via scatter1 node, but in case it is important its value is 12.00.
    
    And now the coolest part follows :)
    
    <a href="https://codeandunicorns.com/wp-content/uploads/2015/07/8viewonendproduct.jpg"><img class="aligncenter wp-image-1285" src="https://codeandunicorns.com/wp-content/uploads/2015/07/8viewonendproduct-1024x543.jpg" alt="8viewonendproduct" width="1100" height="584" /></a>
    
    &nbsp;
    
    Lets take a closer look to 2 specific nodes which make the biggest difference of them all. textpath1 node is a very special node. It is capable of tracing lines of any letter or character in general from at least in theory all supported fonts and UTF-8. As you can see in the properties window you can input Text which will be used by scatter node to populate points on the path of the letters.
    
    <img class="aligncenter wp-image-1286" src="https://codeandunicorns.com/wp-content/uploads/2015/07/9fonttextpath1-1024x543.jpg" alt="9fonttextpath1" width="1163" height="617" />
    
    And a look on scatter node with its config. In this case we used amount of 100 points, which translates in reality in 100 starfish coloured in different shades of colour in a shape of CU (Code and unicorns)
    
    <a href="https://codeandunicorns.com/wp-content/uploads/2015/07/10fontpointbasedsystem.jpg"><img class="aligncenter wp-image-1287" src="https://codeandunicorns.com/wp-content/uploads/2015/07/10fontpointbasedsystem-1024x544.jpg" alt="10fontpointbasedsystem" width="776" height="412" /></a><a href="https://codeandunicorns.com/wp-content/uploads/2015/07/11amountofpoints.jpg"><img class="aligncenter size-full wp-image-1288" src="https://codeandunicorns.com/wp-content/uploads/2015/07/11amountofpoints.jpg" alt="11amountofpoints" width="799" height="928" /></a>
    
    &nbsp;
fusion_builder_converted:
  - 'yes'
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
  - 'no'
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
image: /wp-content/uploads/2015/07/8viewonendproduct.jpg
categories:
  - ALL
---
**What: **

NodeBox is a node-based software application for generative design. It helps designers and everyone that uses it to automate boring productiong challenges, visualise large sets of data and manipulate the raw power of computer without using mechanical language of machines. The tools are able to integrate with traditional design applications and are cross platform.

In my case it was used as a tool for artistic expression and beauty of the heart.

&nbsp;

**Where:**

Main page: <https://www.nodebox.net/node/>

Download: <https://www.nodebox.net/download/>

**The project:**

Explanation of the project itself. followed by through explanation of tutorial with pictures etc explanation of workflows and rendering. It is at least in a nice part based on howtos of <a href="https://www.nodebox.net/node/documentation/tutorial/getting-started.html" target="_blank">Nodebox wikis and tutorial</a>, with some changes to make it more suit to my purpose as for example retracing animations and shapes  by letter shapes, reconfiguring the borders  a few different things on color algorithms, but don&#8217;t worry. We will cover most of the needed things in this tutorial.

&nbsp;

Before we go too into depth I will first try to explain the following graphical representation and a bit about Nodebox 3 specifically at the same time. So, the software itself is meant to be used as a tool toward generative design, mathematical and data representation in a visual way. In this case I had used it as a tool of artistic expression, or at least so I have envisioned my use. Also you can do everything through programming and only Nodebox version 3 enables you to do it in as intuitive and useful way like you can see here. They also offer library for Open GL which is bloody good. Maybe some fun and intriguing use can be found for games or virtual reality ?

&nbsp;

For this tutorial I will also assume basic knowledge and that you have done the official tutorial which is **here** and also part of the references and things that I find connected at the bottom of the article. And for this current variation of nodes, it may help taking the original tutorial and checking the differences or using the following images as better reference and maybe learning in process how to make it your own with some fluffy new funny variations. And **now** directly to the already done node diagram bellow.

&nbsp;

Overral description of the diagram:

You get a number in a defined range from range1 node. Run that number through 3 separate nodes of add1 divide1 and multiply1. From there the new unique numbers continue down the path. One to the wave1 which will take care for wave generation and the wave1 output will be the input of make_point1. Which will actually visualize the dots based on the waveform itself. The divide node is used as a parameters for ellipse1, if i am correct it should be used for width and height.

Ok now lets jump to the right side. Through the colour modes you provide your choice of colours (you can also use RGB nodes if you want instead). From there colour nodes are connected to the combine list and to repeat list. Which basically in practice means that the different make_points will be covered in a certain colour for certain length of points. For example 5 consecutive points&#8230;

From the make_point lover we go to ellipse which just defines the shape of the points, following by colourize which will help us colour the points themselves, via a normal connection like on the picture of a group1 one followed by align1 node. copy1 node settings will be explained more in detail bellow on a separate picture. Via scale1 node you can define the sizes and scalation of your wavy points. If you are wondering what are those lines that go into left upper direction&#8230; they are parent inputs which a parent network of nodes provide to a child network group which is what we see at the moment.

&nbsp;

[<img class="aligncenter size-full wp-image-1278" src="https://codeandunicorns.com/wp-content/uploads/2015/07/1.jpg" alt="1" width="810" height="695" srcset="https://codeandunicorns.com/wp-content/uploads/2015/07/1-300x257.jpg 300w, https://codeandunicorns.com/wp-content/uploads/2015/07/1.jpg 810w" sizes="(max-width: 810px) 100vw, 810px" />](https://codeandunicorns.com/wp-content/uploads/2015/07/1.jpg)

&nbsp;

On the middle top you have range node, which you use through its settings  and manipulate the range of the number generated. From there i sent the number in 3 ways, from addition node to dividing node and multiplying node.

The addition node continues to wave1 form which other argument comes from a parent (Basically you can use grouping for a lot of modes, and use that group as a single node one level up the hierarchy and define which inputs are available from the upper hierarchy down etc. The grouping itself can be done via selection and right click until you see a menu to create a subnetwork). From wave1 node (where you can set up the wave size and repeat period through its parameters &#8211; picture screen can be seen below) which defines the size of a wave we continue to make_point1 which will create actual point themselves.

&nbsp;

[<img class="aligncenter size-full wp-image-1279" src="https://codeandunicorns.com/wp-content/uploads/2015/07/2Capture.jpg" alt="2Capture" width="769" height="416" srcset="https://codeandunicorns.com/wp-content/uploads/2015/07/2Capture-300x162.jpg 300w, https://codeandunicorns.com/wp-content/uploads/2015/07/2Capture.jpg 769w" sizes="(max-width: 769px) 100vw, 769px" />](https://codeandunicorns.com/wp-content/uploads/2015/07/2Capture.jpg)

&nbsp;

Example of used wave1 node with current configuration of sizes period and type.

[<img class="aligncenter size-full wp-image-1280" src="https://codeandunicorns.com/wp-content/uploads/2015/07/3wave1.jpg" alt="3wave1" width="332" height="239" srcset="https://codeandunicorns.com/wp-content/uploads/2015/07/3wave1-300x216.jpg 300w, https://codeandunicorns.com/wp-content/uploads/2015/07/3wave1.jpg 332w" sizes="(max-width: 332px) 100vw, 332px" />](https://codeandunicorns.com/wp-content/uploads/2015/07/3wave1.jpg)

&nbsp;

Exact configuration of copy1 node. If you look closely you can see that I have chosen 9 copies with 40 angle rotation. Due to this node you can create a circley slightly angled starfish like looking structure. It basically takes the wave points created before which were also coloured, takes that makes 9 copies of them and angles everything together around a common centre point.

[<img class="aligncenter size-full wp-image-1281" src="https://codeandunicorns.com/wp-content/uploads/2015/07/4copy1.jpg" alt="4copy1" width="436" height="275" srcset="https://codeandunicorns.com/wp-content/uploads/2015/07/4copy1-300x189.jpg 300w, https://codeandunicorns.com/wp-content/uploads/2015/07/4copy1-320x202.jpg 320w, https://codeandunicorns.com/wp-content/uploads/2015/07/4copy1.jpg 436w" sizes="(max-width: 436px) 100vw, 436px" />](https://codeandunicorns.com/wp-content/uploads/2015/07/4copy1.jpg)

&nbsp;

Ok, the lowest level is finished for the time being. Select all the nodes, press right mouse button and choose Group into Network. and name it a thing. Connect 2 random_numbers nodes and a frame nod like you see on the picture. You can actually ignore the mod and add nodes since I have just forgot to remove them while doing this.

This and the next picture are showing you confighs for random\_numbers1 and random\_numbers2 node configurations which I have chosen. After all is done feel free to play with any configs with keeping the eye on the changes.

<img class="aligncenter size-full wp-image-1282" src="https://codeandunicorns.com/wp-content/uploads/2015/07/5randomnumbers1.jpg" alt="5randomnumbers1" width="903" height="953" srcset="https://codeandunicorns.com/wp-content/uploads/2015/07/5randomnumbers1-284x300.jpg 284w, https://codeandunicorns.com/wp-content/uploads/2015/07/5randomnumbers1.jpg 903w" sizes="(max-width: 903px) 100vw, 903px" /> 

&nbsp;

[<img class="aligncenter size-full wp-image-1283" src="https://codeandunicorns.com/wp-content/uploads/2015/07/6randomnumbers2.jpg" alt="6randomnumbers2" width="746" height="937" srcset="https://codeandunicorns.com/wp-content/uploads/2015/07/6randomnumbers2-239x300.jpg 239w, https://codeandunicorns.com/wp-content/uploads/2015/07/6randomnumbers2.jpg 746w" sizes="(max-width: 746px) 100vw, 746px" />](https://codeandunicorns.com/wp-content/uploads/2015/07/6randomnumbers2.jpg)

Showing the thing config which contains all the low level node configuration seen from earlier.

[<img class="aligncenter size-large wp-image-1284" src="https://codeandunicorns.com/wp-content/uploads/2015/07/7overallview-1024x543.jpg" alt="7overallview" width="669" height="355" srcset="https://codeandunicorns.com/wp-content/uploads/2015/07/7overallview-300x159.jpg 300w, https://codeandunicorns.com/wp-content/uploads/2015/07/7overallview-1024x543.jpg 1024w, https://codeandunicorns.com/wp-content/uploads/2015/07/7overallview.jpg 1918w" sizes="(max-width: 669px) 100vw, 669px" />](https://codeandunicorns.com/wp-content/uploads/2015/07/7overallview.jpg)

And now comes the proper fun part of the tutorial with awesome looks and all the glitter!

Create nodes according to the image bellow.

For the randomnumbers1 values are: 50 min and 500 max

For the randomnumbers2 values are: 0 min and 800 max

For the randomnumbers3 values are: 0.75 min and 4.00 max

For the range1 start is 0.00 and Step property is 1.00.

For the number1 itself I do actually think the number itself is not so important since I circumvented it via scatter1 node, but in case it is important its value is 12.00.

And now the coolest part follows 🙂

[<img class="aligncenter wp-image-1285" src="https://codeandunicorns.com/wp-content/uploads/2015/07/8viewonendproduct-1024x543.jpg" alt="8viewonendproduct" width="1100" height="584" srcset="https://codeandunicorns.com/wp-content/uploads/2015/07/8viewonendproduct-300x159.jpg 300w, https://codeandunicorns.com/wp-content/uploads/2015/07/8viewonendproduct-1024x543.jpg 1024w, https://codeandunicorns.com/wp-content/uploads/2015/07/8viewonendproduct.jpg 1919w" sizes="(max-width: 1100px) 100vw, 1100px" />](https://codeandunicorns.com/wp-content/uploads/2015/07/8viewonendproduct.jpg)

&nbsp;

Lets take a closer look to 2 specific nodes which make the biggest difference of them all. textpath1 node is a very special node. It is capable of tracing lines of any letter or character in general from at least in theory all supported fonts and UTF-8. As you can see in the properties window you can input Text which will be used by scatter node to populate points on the path of the letters.

<img class="aligncenter wp-image-1286" src="https://codeandunicorns.com/wp-content/uploads/2015/07/9fonttextpath1-1024x543.jpg" alt="9fonttextpath1" width="1163" height="617" srcset="https://codeandunicorns.com/wp-content/uploads/2015/07/9fonttextpath1-300x159.jpg 300w, https://codeandunicorns.com/wp-content/uploads/2015/07/9fonttextpath1-1024x543.jpg 1024w, https://codeandunicorns.com/wp-content/uploads/2015/07/9fonttextpath1.jpg 1913w" sizes="(max-width: 1163px) 100vw, 1163px" /> 

And a look on scatter node with its config. In this case we used amount of 100 points, which translates in reality in 100 starfish coloured in different shades of colour in a shape of CU (Code and unicorns)

[<img class="aligncenter wp-image-1287" src="https://codeandunicorns.com/wp-content/uploads/2015/07/10fontpointbasedsystem-1024x544.jpg" alt="10fontpointbasedsystem" width="776" height="412" srcset="https://codeandunicorns.com/wp-content/uploads/2015/07/10fontpointbasedsystem-300x159.jpg 300w, https://codeandunicorns.com/wp-content/uploads/2015/07/10fontpointbasedsystem-1024x544.jpg 1024w, https://codeandunicorns.com/wp-content/uploads/2015/07/10fontpointbasedsystem.jpg 1915w" sizes="(max-width: 776px) 100vw, 776px" />](https://codeandunicorns.com/wp-content/uploads/2015/07/10fontpointbasedsystem.jpg)[<img class="aligncenter size-full wp-image-1288" src="https://codeandunicorns.com/wp-content/uploads/2015/07/11amountofpoints.jpg" alt="11amountofpoints" width="799" height="928" srcset="https://codeandunicorns.com/wp-content/uploads/2015/07/11amountofpoints-258x300.jpg 258w, https://codeandunicorns.com/wp-content/uploads/2015/07/11amountofpoints.jpg 799w" sizes="(max-width: 799px) 100vw, 799px" />](https://codeandunicorns.com/wp-content/uploads/2015/07/11amountofpoints.jpg)

&nbsp;