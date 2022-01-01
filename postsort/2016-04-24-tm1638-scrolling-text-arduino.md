---
id: 1772
title: TM1638 Scrolling text on Arduino
date: 2016-04-24T18:18:31+00:00
author: Matjaz Trcek
layout: post
guid: https://codeandunicorns.com/?p=1772
permalink: /tm1638-scrolling-text-arduino/
slide_template:
  - default
fusion_builder_status:
  - inactive
avada_post_views_count:
  - "14869"
dsq_thread_id:
  - "4773065319"
fusion_builder_content_backup:
  - |
    The following explanation of the code and how it works and how to connect TM1638
    (with led array, display and button array) to Arduino.
    For IDE and project Initialization I used PlatformIO and due to that and since it makes lots of stuff easier it generates project in C++ with lots os useful configs pre-prepared and if your using Git you will find already prepared .git-ignore file in project as well.
    <h2><strong>Video example:</strong></h2>
    <p style="text-align: center;">[youtube id="guVrI-0o5OE" width="600" height="350" autoplay="no" api_params="" class=""]</p>
    
    <h2></h2>
    <h2><strong>Code explanation:</strong></h2>
    In following code you can see the imports which I used, from Arduino lib which you can ignore if you are using Native IDE.
    Regarding TM1638.h you can get it on <a href="https://github.com/rjbatista/tm1638-library">THIS Github</a> and add it in Platformio under lib or in native IDE under libraries folder.
    
    [code lang="cpp"]
    #include &quot;Arduino.h&quot;
    #include &lt;TM1638.h&gt;
    [/code]
    
    Now comes the variable initialisation part.
    As seen on the video we connect the wires to 8,9,10 pins on TM1638 with TM1638 module(8, 9, 10); command.
    For default interval I have chosen 1000ms which is the rate before it moves letters one forward for scrolling.
    String textScroll is a variable containing the text that will get displayed on the display.
    bckp variable will be used for reinitializing the text after it scrolled through. It may not be the best way of doing it since later we are popping letters out of string, but I tried to minize the amount of code and kinda simplify it :D
    Well buttons variable should be quite obvious so let's continue to final previousMillis variable.
    This variable will be used for helping to detect button press between moving the display letters. That's because if we would use <strong>Delay</strong> command we would be essentially stopping the clock and unable to detect button press, or a lot harder and unintuitive to detect them.
    
    [code lang="cpp"]
    // define a module on data pin 8, clock pin 9 and strobe pin 10
    TM1638 module(8, 9, 10);
    long interval=1000;
    String textScroll=&quot;This is long sentence&quot;;
    String bckp;
    byte buttons;
    unsigned long previousMillis = 0;
    [/code]
    
    In setup loop we only set textScroll string to bckp string variable so we can restore text after we pop up the whole string.
    
    [code lang="cpp"]
    void setup()
    {
    bckp = textScroll;
    }
    [/code]
    
    Start of the main loop:
    In the main loop we start with setDisplayToString through which we connect to TM1638 module and set the string variable. After that we date our currentMillis to get millisecond amount which passed. We compare that in the IF statement and check if the difference is bigger then interval that is determined in the variable (P.S. later we configure interval to be adjustable). The next line is just updating previousMillis to currentMillis to reset the counter for next time.
    After that we finally get to the interesting part.
    In <strong>if(textScroll.length()&gt;0</strong> we check if string variable length is bigger than 0 and if it is then we remove the first character of the string and re-show it on display of TM1638 with clearDisplayDigitclearDisplayDigit
    
    [code lang="cpp"]
    void loop()
    {
    
    module.setDisplayToString(textScroll);
    unsigned long currentMillis = millis();
    
    if (currentMillis - previousMillis &gt;= interval) {
    // save the last time you blinked the LED
    previousMillis = currentMillis;
    if(textScroll.length()&gt;0){
    textScroll.remove(0, 1);
    if(textScroll.length()&lt;8){
    module.clearDisplayDigit(textScroll.length(), false);
    }
    } else {
    textScroll = bckp;
    }
    }
    [/code]
    
    The most important code of scrolling text is now over, but here is some extra code regarding turning LED's ON with buttons and changing the interval time for text scrolling
    
    [code lang="cpp"]
    buttons=module.getButtons();
    if(buttons==1) {
    module.setLED(TM1638_COLOR_RED, 0);
    interval=500;
    delay(100);
    }if (buttons==4) {
    module.setLED(TM1638_COLOR_RED, 2);
    interval=1500;
    delay(100);
    }if (buttons==8) {
    module.setLED(TM1638_COLOR_RED, 3);
    interval=2500;
    delay(100);
    }
    module.setLED(0, 0);
    module.setLED(0, 2);
    module.setLED(0, 3);
    
    }
    [/code]
    
    <h2></h2>
    <h2><strong>Full code:</strong></h2>
    In code bellow you can see full united code. You can also see everything in a sample project under <a href="https://github.com/mitola/tm1638-text-scrolling-arduino">THIS URL in Github</a>.
    
    [code lang="cpp"]
    #include &quot;Arduino.h&quot;
    #include &lt;TM1638.h&gt;
    
    // define a module on data pin 8, clock pin 9 and strobe pin 10
    TM1638 module(8, 9, 10);
    long interval=1000;
    String textScroll=&quot;This is long sentence&quot;;
    String bckp;
    byte buttons;
    unsigned long previousMillis = 0;
    
    void setup()
    {
    bckp = textScroll;
    }
    
    void loop()
    {
    
    module.setDisplayToString(textScroll);
    unsigned long currentMillis = millis();
    
    if (currentMillis - previousMillis &amp;gt;= interval) {
    // save the last time you blinked the LED
    previousMillis = currentMillis;
    if(textScroll.length()&gt;0){
    textScroll.remove(0, 1);
    if(textScroll.length()&lt;8){
    module.clearDisplayDigit(textScroll.length(), false);
    }
    } else {
    textScroll = bckp;
    }
    }
    
    buttons=module.getButtons();
    if(buttons==1) {
    module.setLED(TM1638_COLOR_RED, 0);
    interval=500;
    delay(100);
    }if (buttons==4) {
    module.setLED(TM1638_COLOR_RED, 2);
    interval=1500;
    delay(100);
    }if (buttons==8) {
    module.setLED(TM1638_COLOR_RED, 3);
    interval=2500;
    delay(100);
    }
    module.setLED(0, 0);
    module.setLED(0, 2);
    module.setLED(0, 3);
    
    }
    
    [/code]
    
fusion_builder_converted:
  - 'yes'
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
  - 'no'
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
sbg_selected_sidebar:
  - 'a:1:{i:0;s:1:"0";}'
sbg_selected_sidebar_replacement:
  - 'a:1:{i:0;s:12:"Blog Sidebar";}'
sbg_selected_sidebar_2:
  - 'a:1:{i:0;s:1:"0";}'
sbg_selected_sidebar_2_replacement:
  - 'a:1:{i:0;s:0:"";}'
pyre_sidebar_sticky:
  - default
pyre_page_title_line_height:
  - ""
kd_featured-image-2_post_id:
  - ""
kd_featured-image-3_post_id:
  - ""
kd_featured-image-4_post_id:
  - ""
kd_featured-image-5_post_id:
  - ""
image: /wp-content/uploads/2016/04/TM1638_with_arduino_scroll-min.jpg
categories:
  - ALL
  - Electronics
  - How to
tags:
  - arduino
  - programming
  - TM1638
---
The following explanation of the code and how it works and how to connect TM1638  
(with led array, display and button array) to Arduino.  
For IDE and project Initialization I used PlatformIO and due to that and since it makes lots of stuff easier it generates project in C++ with lots os useful configs pre-prepared and if your using Git you will find already prepared .git-ignore file in project as well.

## **Video example:**

<p style="text-align: center;">
  <div  class="fusion-fullwidth fullwidth-box hundred-percent-fullwidth"  style='background-color: #ffffff;background-position: center center;background-repeat: no-repeat;padding-top:0px;padding-right:0px;padding-bottom:0px;padding-left:0px;'>
    <div class="fusion-builder-row fusion-row ">
      <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
        <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
          <div class="fusion-video fusion-youtube" style="max-width:600px;max-height:350px;">
            <div class="video-shortcode">
            </div>
          </div>
          
          <h2>
          </h2>
          
          <h2>
            <strong>Code explanation:</strong>
          </h2>
          
          <p>
            In following code you can see the imports which I used, from Arduino lib which you can ignore if you are using Native IDE.<br /> Regarding TM1638.h you can get it on <a href="https://github.com/rjbatista/tm1638-library">THIS Github</a> and add it in Platformio under lib or in native IDE under libraries folder.
          </p>
          
          <div class="fusion-clearfix">
          </div>
        </div>
      </div>
      
      <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
        <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
          <pre class="brush: cpp; title: ; notranslate" title="">
#include "Arduino.h"
#include &lt;TM1638.h&gt;
</pre>
          
          <p>
            Now comes the variable initialisation part.<br /> As seen on the video we connect the wires to 8,9,10 pins on TM1638 with TM1638 module(8, 9, 10); command.<br /> For default interval I have chosen 1000ms which is the rate before it moves letters one forward for scrolling.<br /> String textScroll is a variable containing the text that will get displayed on the display.<br /> bckp variable will be used for reinitializing the text after it scrolled through. It may not be the best way of doing it since later we are popping letters out of string, but I tried to minize the amount of code and kinda simplify it 😀<br /> Well buttons variable should be quite obvious so let&#8217;s continue to final previousMillis variable.<br /> This variable will be used for helping to detect button press between moving the display letters. That&#8217;s because if we would use <strong>Delay</strong> command we would be essentially stopping the clock and unable to detect button press, or a lot harder and unintuitive to detect them.
          </p>
          
          <div class="fusion-clearfix">
          </div>
        </div>
      </div>
      
      <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
        <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
          <pre class="brush: cpp; title: ; notranslate" title="">
// define a module on data pin 8, clock pin 9 and strobe pin 10
TM1638 module(8, 9, 10);
long interval=1000;
String textScroll="This is long sentence";
String bckp;
byte buttons;
unsigned long previousMillis = 0;
</pre>
          
          <p>
            In setup loop we only set textScroll string to bckp string variable so we can restore text after we pop up the whole string.
          </p>
          
          <div class="fusion-clearfix">
          </div>
        </div>
      </div>
      
      <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
        <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
          <pre class="brush: cpp; title: ; notranslate" title="">
void setup()
{
  bckp = textScroll;
}
</pre>
          
          <p>
            Start of the main loop:<br /> In the main loop we start with setDisplayToString through which we connect to TM1638 module and set the string variable. After that we date our currentMillis to get millisecond amount which passed. We compare that in the IF statement and check if the difference is bigger then interval that is determined in the variable (P.S. later we configure interval to be adjustable). The next line is just updating previousMillis to currentMillis to reset the counter for next time.<br /> After that we finally get to the interesting part.<br /> In <strong>if(textScroll.length()>0</strong> we check if string variable length is bigger than 0 and if it is then we remove the first character of the string and re-show it on display of TM1638 with clearDisplayDigitclearDisplayDigit
          </p>
          
          <div class="fusion-clearfix">
          </div>
        </div>
      </div>
      
      <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
        <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
          <pre class="brush: cpp; title: ; notranslate" title="">
void loop()
{

module.setDisplayToString(textScroll);
unsigned long currentMillis = millis();

if (currentMillis - previousMillis &gt;= interval) {
  // save the last time you blinked the LED
  previousMillis = currentMillis;
  if(textScroll.length()&gt;0){
    textScroll.remove(0, 1);
    if(textScroll.length()&lt;8){
      module.clearDisplayDigit(textScroll.length(), false);
    }
  } else {
    textScroll = bckp;
  }
}
</pre>
          
          <p>
            The most important code of scrolling text is now over, but here is some extra code regarding turning LED&#8217;s ON with buttons and changing the interval time for text scrolling
          </p>
          
          <div class="fusion-clearfix">
          </div>
        </div>
      </div>
      
      <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
        <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
          <pre class="brush: cpp; title: ; notranslate" title="">
buttons=module.getButtons();
if(buttons==1) {
  module.setLED(TM1638_COLOR_RED, 0);
  interval=500;
  delay(100);
}if (buttons==4) {
  module.setLED(TM1638_COLOR_RED, 2);
  interval=1500;
  delay(100);
}if (buttons==8) {
  module.setLED(TM1638_COLOR_RED, 3);
  interval=2500;
  delay(100);
}
module.setLED(0, 0);
module.setLED(0, 2);
module.setLED(0, 3);

}
</pre>
          
          <h2>
          </h2>
          
          <h2>
            <strong>Full code:</strong>
          </h2>
          
          <p>
            In code bellow you can see full united code. You can also see everything in a sample project under <a href="https://github.com/mitola/tm1638-text-scrolling-arduino">THIS URL in Github</a>.
          </p>
          
          <div class="fusion-clearfix">
          </div>
        </div>
      </div>
      
      <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
        <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
          <pre class="brush: cpp; title: ; notranslate" title="">
#include "Arduino.h"
#include &lt;TM1638.h&gt;

// define a module on data pin 8, clock pin 9 and strobe pin 10
TM1638 module(8, 9, 10);
long interval=1000;
String textScroll="This is long sentence";
String bckp;
byte buttons;
unsigned long previousMillis = 0;

void setup()
{
  bckp = textScroll;
}

void loop()
{

module.setDisplayToString(textScroll);
unsigned long currentMillis = millis();

if (currentMillis - previousMillis &gt;= interval) {
  // save the last time you blinked the LED
  previousMillis = currentMillis;
  if(textScroll.length()&gt;0){
    textScroll.remove(0, 1);
    if(textScroll.length()&lt;8){
      module.clearDisplayDigit(textScroll.length(), false);
    }
  } else {
    textScroll = bckp;
  }
}

buttons=module.getButtons();
if(buttons==1) {
  module.setLED(TM1638_COLOR_RED, 0);
  interval=500;
  delay(100);
}if (buttons==4) {
  module.setLED(TM1638_COLOR_RED, 2);
  interval=1500;
  delay(100);
}if (buttons==8) {
  module.setLED(TM1638_COLOR_RED, 3);
  interval=2500;
  delay(100);
}
module.setLED(0, 0);
module.setLED(0, 2);
module.setLED(0, 3);

}

</pre>
          
          <div class="fusion-clearfix">
          </div>
        </div>
      </div>
    </div>
  </div>
</p>