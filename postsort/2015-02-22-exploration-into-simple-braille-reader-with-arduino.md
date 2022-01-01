---
id: 971
title: Exploration into simple Braille reader with Arduino
date: 2015-02-22T20:07:06+00:00
author: Matjaz Trcek
layout: post
guid: http://codeandunicorns.com/?p=971
permalink: /exploration-into-simple-braille-reader-with-arduino/
slide_template:
  - default
pyre_full_width:
  - 'no'
pyre_transparent_header:
  - default
avada_post_views_count:
  - "6142"
dsq_thread_id:
  - "4723162384"
fusion_builder_content_backup:
  - |
    <a href="http://codeandunicorns.com/wp-content/uploads/2015/02/braille-99020_640.png">
    </a>
    If you ever checked for Braille displays you may noticed they are terribly expensive. A "normal" one with a good sentence of characters can cost in thousands of dollars. Which is well quite expensive. So it got me thinking what I could do to make a basic Braille display which could potentially be a lot more cost effective?
    
    And I dived into imaginary world of Arduino where I wrote a very basic representation of the logic. Even though it uses a basic LED array it is meant as a representation of Braille character, which is 6 bit and one character can be easily represented with 6 LED lights.
    
    I used first dots on the top as LED 1 and LED 2 , the middle ones for LED 3 and LED 4 and the same for last 2(Braille code at the bottom of -&gt; <a href="http://en.wikipedia.org/wiki/Six-bit_character_code">this link</a>).
    The basic idea is that you use something like for example <a href="http://www.microsoft.com/enable/default.aspx">Microsoft Accessibility API</a> through which you would send data to something like an Arduino or custom made circuit board connected with for example 6 electromechanical Braille dot "one-character displays".
    What would be the best thing to use for the Braille part of components is debatable and there are multiple ways of doing it.
    
    With usage of Arduino and most probably custom ordered parts for Braille could potentially give you a basic reader of 12 characters for around 100-150 euros.
    
    In the second part of the article you can check references, video example with Arduino and the code used for the particular example as seen.
    
    References and extra literature:
    
    -<a href="http://www.cim.mcgill.ca/~haptic/pub/VL-JP-VH-WH-07.pdf">Braille Display by Lateral Skin Deformation with the STReSS2 Tactile Transducer</a>
    -<a href="http://en.wikipedia.org/wiki/Six-bit_character_code">Six-bit character code
    </a>-<a href="http://www.google.de/patents/US3230644">Electronic braille instructor / patent
    </a>-<a href="https://www.google.de/patents/US4473356?dq=braille&amp;hl=en&amp;sa=X&amp;ei=yBTqVJHHFMWkPIHggVg&amp;ved=0CEwQ6AEwBg">Electromechanical braille cell and method of operating same / patent
    </a>-<a href="http://www.kscitech.com/BC/D/Braille_cell/">Braille Cell &amp; Refreshable Braille Display Design Data</a>
    
    My Arduino video example with a LED array for representation of CODE&amp;UNICORNS keyword. SHould be filmed from reverse perspective, but you get an idea.
    [youtube id="geHzq9dog6g" width="600" height="350" autoplay="no" api_params="" class=""]
    
    [code language="C"]
    //******************************************************//
    // Define key pin - Names like on the board
    int K1 = 13;
    int K2 = 12;
    int K3 = 11;
    int K4 = 10;
    // Define led pin
    int GND = 6;
    int D1 = 5;
    int D2 = 4;
    int D3 = 3;
    int D4 = 2;
    int D5 = 1;
    int D6 = 0;
    // variables will change:
    int buttonState = 0; // variable for reading the pushbutton status
    // the setup routine runs once when you press reset:
    
    void setup() {
    // initialize the keys pin as an input.
    pinMode(K1, INPUT);
    pinMode(K2, INPUT);
    pinMode(K3, INPUT);
    pinMode(K4, INPUT);
    // initialize the leds pin as an output.
    pinMode(GND, OUTPUT);
    pinMode(D1, OUTPUT);
    pinMode(D2, OUTPUT);
    pinMode(D3, OUTPUT);
    pinMode(D4, OUTPUT);
    pinMode(D5, OUTPUT);
    pinMode(D6, OUTPUT);
    //Activate key pin internal pull-up resistors
    digitalWrite(K1, HIGH);
    digitalWrite(K2, HIGH);
    digitalWrite(K3, HIGH);
    digitalWrite(K4, HIGH);
    //as LED GND
    digitalWrite(GND, LOW);
    }
    
    // the loop routine runs over and over again forever:
    void loop() {
    buttonState = digitalRead(K1); //reading input of the first button
    if (buttonState == LOW) {
    // Code and unicorns in Braile writting
    //parameters are for D1,D2,D3,D4,D5,D6 status
    letterPrint(1,1,0,0,0,0);//C
    letterPrint(1,0,0,1,1,0);//O
    letterPrint(1,1,0,1,0,0);//D
    letterPrint(1,0,0,1,0,0);//E
    letterPrint(1,1,1,0,1,1);//&amp;
    letterPrint(1,0,0,0,1,1);//U
    letterPrint(1,1,0,1,1,0);//N
    letterPrint(0,1,1,0,0,0);//I
    letterPrint(1,1,0,0,0,0);//C
    letterPrint(1,0,0,1,1,0);//O
    letterPrint(1,0,1,1,1,0);//R
    letterPrint(1,1,0,1,1,0);//N
    letterPrint(0,1,1,0,1,0);//S
    }
    }
    
    //Function that takes 6 numeric values and uses them to sent voltage to the designated pin as per variable. That consequentially make LED turn on.
    void letterPrint(int d1sta,int d2sta,int d3sta,int d4sta,int d5sta,int d6sta) {
    digitalWrite(D1, d1sta);
    digitalWrite(D2, d2sta);
    digitalWrite(D3, d3sta);
    digitalWrite(D4, d4sta);
    digitalWrite(D5, d5sta);
    digitalWrite(D6, d6sta);
    delay(1000);
    }
    [/code]
    
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
image: /wp-content/uploads/2015/02/braille-99020_640-e1425124240757.png
categories:
  - ALL
  - How to
---
[  
](http://codeandunicorns.com/wp-content/uploads/2015/02/braille-99020_640.png)  
If you ever checked for Braille displays you may noticed they are terribly expensive. A &#8220;normal&#8221; one with a good sentence of characters can cost in thousands of dollars. Which is well quite expensive. So it got me thinking what I could do to make a basic Braille display which could potentially be a lot more cost effective?

And I dived into imaginary world of Arduino where I wrote a very basic representation of the logic. Even though it uses a basic LED array it is meant as a representation of Braille character, which is 6 bit and one character can be easily represented with 6 LED lights.

I used first dots on the top as LED 1 and LED 2 , the middle ones for LED 3 and LED 4 and the same for last 2(Braille code at the bottom of -> [this link](http://en.wikipedia.org/wiki/Six-bit_character_code)).  
The basic idea is that you use something like for example [Microsoft Accessibility API](http://www.microsoft.com/enable/default.aspx) through which you would send data to something like an Arduino or custom made circuit board connected with for example 6 electromechanical Braille dot &#8220;one-character displays&#8221;.  
What would be the best thing to use for the Braille part of components is debatable and there are multiple ways of doing it.

With usage of Arduino and most probably custom ordered parts for Braille could potentially give you a basic reader of 12 characters for around 100-150 euros.

In the second part of the article you can check references, video example with Arduino and the code used for the particular example as seen.

References and extra literature:

&#8211;[Braille Display by Lateral Skin Deformation with the STReSS2 Tactile Transducer](http://www.cim.mcgill.ca/~haptic/pub/VL-JP-VH-WH-07.pdf)  
&#8211;[Six-bit character code  
](http://en.wikipedia.org/wiki/Six-bit_character_code) &#8211;[Electronic braille instructor / patent  
](http://www.google.de/patents/US3230644) &#8211;[Electromechanical braille cell and method of operating same / patent  
](https://www.google.de/patents/US4473356?dq=braille&hl=en&sa=X&ei=yBTqVJHHFMWkPIHggVg&ved=0CEwQ6AEwBg) &#8211;[Braille Cell & Refreshable Braille Display Design Data](http://www.kscitech.com/BC/D/Braille_cell/)

My Arduino video example with a LED array for representation of CODE&UNICORNS keyword. SHould be filmed from reverse perspective, but you get an idea.  


<div  class="fusion-fullwidth fullwidth-box hundred-percent-fullwidth"  style='background-color: #ffffff;background-position: center center;background-repeat: no-repeat;padding-top:0px;padding-right:0px;padding-bottom:0px;padding-left:0px;'>
  <div class="fusion-builder-row fusion-row ">
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <div class="fusion-video fusion-youtube" style="max-width:600px;max-height:350px;">
          <div class="video-shortcode">
          </div>
        </div>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: cpp; title: ; notranslate" title="">
//******************************************************//
// Define key pin - Names like on the board
int K1 = 13;
int K2 = 12;
int K3 = 11;
int K4 = 10;
// Define led pin
int GND = 6;
int D1 = 5;
int D2 = 4;
int D3 = 3;
int D4 = 2;
int D5 = 1;
int D6 = 0;
// variables will change:
int buttonState = 0; // variable for reading the pushbutton status
// the setup routine runs once when you press reset:

void setup() {
  // initialize the keys pin as an input.
  pinMode(K1, INPUT);
  pinMode(K2, INPUT);
  pinMode(K3, INPUT);
  pinMode(K4, INPUT);
  // initialize the leds pin as an output.
  pinMode(GND, OUTPUT);
  pinMode(D1, OUTPUT);
  pinMode(D2, OUTPUT);
  pinMode(D3, OUTPUT);
  pinMode(D4, OUTPUT);
  pinMode(D5, OUTPUT);
  pinMode(D6, OUTPUT);
  //Activate key pin internal pull-up resistors
  digitalWrite(K1, HIGH);
  digitalWrite(K2, HIGH);
  digitalWrite(K3, HIGH);
  digitalWrite(K4, HIGH);
  //as LED GND
  digitalWrite(GND, LOW);
}

// the loop routine runs over and over again forever:
void loop() {
  buttonState = digitalRead(K1); //reading input of the first button
  if (buttonState == LOW) {
    // Code and unicorns in Braile writting
    //parameters are for D1,D2,D3,D4,D5,D6 status
    letterPrint(1,1,0,0,0,0);//C
    letterPrint(1,0,0,1,1,0);//O
    letterPrint(1,1,0,1,0,0);//D
    letterPrint(1,0,0,1,0,0);//E
    letterPrint(1,1,1,0,1,1);//&
    letterPrint(1,0,0,0,1,1);//U
    letterPrint(1,1,0,1,1,0);//N
    letterPrint(0,1,1,0,0,0);//I
    letterPrint(1,1,0,0,0,0);//C
    letterPrint(1,0,0,1,1,0);//O
    letterPrint(1,0,1,1,1,0);//R
    letterPrint(1,1,0,1,1,0);//N
    letterPrint(0,1,1,0,1,0);//S
  }
}

//Function that takes 6 numeric values and uses them to sent voltage to the designated pin as per variable. That consequentially make LED turn on.
void letterPrint(int d1sta,int d2sta,int d3sta,int d4sta,int d5sta,int d6sta) {
    digitalWrite(D1, d1sta);
    digitalWrite(D2, d2sta);
    digitalWrite(D3, d3sta);
    digitalWrite(D4, d4sta);
    digitalWrite(D5, d5sta);
    digitalWrite(D6, d6sta);
    delay(1000);
}
</pre>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
  </div>
</div>