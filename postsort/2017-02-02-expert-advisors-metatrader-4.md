---
id: 2069
title: Expert Advisors on Metatrader 4
date: 2017-02-02T22:53:25+00:00
author: Joao Pereira
layout: post
guid: https://codeandunicorns.com/?p=2069
permalink: /expert-advisors-metatrader-4/
slide_template:
  - default
fusion_builder_status:
  - ""
avada_post_views_count:
  - "5207"
dsq_thread_id:
  - "5516799332"
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
categories:
  - ALL
  - How to
---
The well known Metatrader 4 (**MT4**) is a well adopted tool in the world of forex trading. It had such a growing success that it is still preferred to the new Metatrader 5. Besides allowing setting up orders it also contains most of the common indicators used in trading. But what caught my eye was the ability to actually code the so-called expert advisors (**EA**) to intervene or to analyse on quote data.

Today I decided to show you a few things I&#8217;ve been learning about MT4&#8217;s ecosystem and how to get started on setting up your own expert advisors.

First lets talk a bit about MT4&#8217;s integrated language **MQL4**:

  * Good for coders familiar with C/C++. Not hard to learn if you&#8217;re used to other typed languages.
  * The official documentation is quite good.
  * There are few communities online you can find snippets and trading strategies.
  * The debug tools on MT4 aren&#8217;t that great.

Honestly I believe anyone with the will can learn a bit of MQL4. After a while you get you used to it, it&#8217;s not of course comparable to more up to date editors but still ok.

The setup can be a bit unusual if you&#8217;re on a Mac. Normally I use my VPS with Windows to do all my work on MT4 but if you are already subscribed to a forex broker I suggest you grab the off-the-shelf VM they usually offer for Mac users. It&#8217;s possible to navigate the VM by accessing it through your applications and click _**Show Package Contents**_. Most of the time you won&#8217;t need to navigate through the explorer to manage files but in case you&#8217;re curious the files are usually stored in something like:

> Contents/Resources/drive_c/Program Files/MT4/MQL4

The easiest way to create an EA is to simply click _**Create in MetaEditor**_ and follow the wizard &#8211; _**Expert Advisor (template)**_. Don&#8217;t be too worried for now on the options presented, you can name it _hello_world_ and pick _onTester_ as the template. You should reach something like this:

<div id="attachment_2079" style="width: 838px" class="wp-caption aligncenter">
  <a href="https://codeandunicorns.com/wp-content/uploads/2017/02/Screen-Shot-2017-02-02-at-20.23.23.png"><img class="wp-image-2079" src="https://codeandunicorns.com/wp-content/uploads/2017/02/Screen-Shot-2017-02-02-at-20.23.23-1024x476.png" alt="Screen Shot 2017-02-02 at 20.23.23" width="828" height="385" srcset="https://codeandunicorns.com/wp-content/uploads/2017/02/Screen-Shot-2017-02-02-at-20.23.23-200x93.png 200w, https://codeandunicorns.com/wp-content/uploads/2017/02/Screen-Shot-2017-02-02-at-20.23.23-300x139.png 300w, https://codeandunicorns.com/wp-content/uploads/2017/02/Screen-Shot-2017-02-02-at-20.23.23-400x186.png 400w, https://codeandunicorns.com/wp-content/uploads/2017/02/Screen-Shot-2017-02-02-at-20.23.23-600x279.png 600w, https://codeandunicorns.com/wp-content/uploads/2017/02/Screen-Shot-2017-02-02-at-20.23.23-768x357.png 768w, https://codeandunicorns.com/wp-content/uploads/2017/02/Screen-Shot-2017-02-02-at-20.23.23-800x372.png 800w, https://codeandunicorns.com/wp-content/uploads/2017/02/Screen-Shot-2017-02-02-at-20.23.23-1024x476.png 1024w, https://codeandunicorns.com/wp-content/uploads/2017/02/Screen-Shot-2017-02-02-at-20.23.23-1200x558.png 1200w" sizes="(max-width: 828px) 100vw, 828px" /></a>
  
  <p class="wp-caption-text">
    Fig. 1 &#8211; Setting up a new Expert Advisor
  </p>
</div>

Don&#8217;t be alarmed by the amount of code present on the template, we&#8217;ll look into a bit of that soon.

After you&#8217;ve created your new EA you can then easily open the EA editor by right clicking on it on the left pane of MT4 and click _**Modify**_.

<div id="attachment_2098" style="width: 447px" class="wp-caption aligncenter">
  <a href="https://codeandunicorns.com/wp-content/uploads/2017/02/screenshot2.png"><img class="wp-image-2098" src="https://codeandunicorns.com/wp-content/uploads/2017/02/screenshot2-783x1024.png" alt="screenshot2" width="437" height="572" srcset="https://codeandunicorns.com/wp-content/uploads/2017/02/screenshot2-200x262.png 200w, https://codeandunicorns.com/wp-content/uploads/2017/02/screenshot2-229x300.png 229w, https://codeandunicorns.com/wp-content/uploads/2017/02/screenshot2-400x523.png 400w, https://codeandunicorns.com/wp-content/uploads/2017/02/screenshot2-600x785.png 600w, https://codeandunicorns.com/wp-content/uploads/2017/02/screenshot2-768x1005.png 768w, https://codeandunicorns.com/wp-content/uploads/2017/02/screenshot2-783x1024.png 783w, https://codeandunicorns.com/wp-content/uploads/2017/02/screenshot2-800x1046.png 800w, https://codeandunicorns.com/wp-content/uploads/2017/02/screenshot2.png 1133w" sizes="(max-width: 437px) 100vw, 437px" /></a>
  
  <p class="wp-caption-text">
    Fig. 2 &#8211; Accessing EA through the main screen
  </p>
</div>

Now that we are set lets have a look on how we can start coding a nice EA.

For starters we will need an entry point function. Going back to our EA lets briefly scroll through the presented options and get to know them:

  * OnInit &#8211; <span class="f_Text"> Constructor. </span>
  * OnDeinit &#8211; Destructor.
  * OnTick &#8211; a _Tick_<span class="f_Text"> event is generated </span><span class="f_Text">when a new tick for a symbol is received. Seems like we can access tick data here.</span>
  * OnTimer &#8211; Function used for initialisation.

Basically these are all event handling functions which allow interface between the MT4 platform and our program. We could easily for example create our &#8220;Hello World!&#8221; using the _OnTick_ function like so:

<div id="attachment_2081" style="width: 401px" class="wp-caption aligncenter">
  <a href="https://codeandunicorns.com/wp-content/uploads/2017/02/Screen-Shot-2017-02-02-at-21.42.11.png"><img class="wp-image-2081" src="https://codeandunicorns.com/wp-content/uploads/2017/02/Screen-Shot-2017-02-02-at-21.42.11-1024x233.png" alt="Screen Shot 2017-02-02 at 21.42.11" width="391" height="89" srcset="https://codeandunicorns.com/wp-content/uploads/2017/02/Screen-Shot-2017-02-02-at-21.42.11-200x46.png 200w, https://codeandunicorns.com/wp-content/uploads/2017/02/Screen-Shot-2017-02-02-at-21.42.11-300x68.png 300w, https://codeandunicorns.com/wp-content/uploads/2017/02/Screen-Shot-2017-02-02-at-21.42.11-400x91.png 400w, https://codeandunicorns.com/wp-content/uploads/2017/02/Screen-Shot-2017-02-02-at-21.42.11-600x137.png 600w, https://codeandunicorns.com/wp-content/uploads/2017/02/Screen-Shot-2017-02-02-at-21.42.11-768x175.png 768w, https://codeandunicorns.com/wp-content/uploads/2017/02/Screen-Shot-2017-02-02-at-21.42.11-800x182.png 800w, https://codeandunicorns.com/wp-content/uploads/2017/02/Screen-Shot-2017-02-02-at-21.42.11-1024x233.png 1024w, https://codeandunicorns.com/wp-content/uploads/2017/02/Screen-Shot-2017-02-02-at-21.42.11.png 1142w" sizes="(max-width: 391px) 100vw, 391px" /></a>
  
  <p class="wp-caption-text">
    Fig. 3 &#8211; Printing Hello World
  </p>
</div>

If you compile the code ([<img class="alignnone wp-image-2072" src="https://codeandunicorns.com/wp-content/uploads/2017/01/Screen-Shot-2017-01-31-at-23.17.04.png" alt="Screen Shot 2017-01-31 at 23.17.04" width="39" height="14" srcset="https://codeandunicorns.com/wp-content/uploads/2017/01/Screen-Shot-2017-01-31-at-23.17.04-150x54.png 150w, https://codeandunicorns.com/wp-content/uploads/2017/01/Screen-Shot-2017-01-31-at-23.17.04.png 152w" sizes="(max-width: 39px) 100vw, 39px" />](https://codeandunicorns.com/wp-content/uploads/2017/01/Screen-Shot-2017-01-31-at-23.17.04.png) on top) you now have your first &#8220;Hello World!&#8221; program! Too bad it&#8217;s not working yet. To make it work we now must return to MT4 main screen and press _**Attach to a chart**_. And voilá! You should see your &#8220;Hello World&#8221; displaying on the _Experts_ tab below.

<div id="attachment_2099" style="width: 420px" class="wp-caption aligncenter">
  <a href="https://codeandunicorns.com/wp-content/uploads/2017/02/screenshot-12.png"><img class="wp-image-2099" src="https://codeandunicorns.com/wp-content/uploads/2017/02/screenshot-12-689x1024.png" alt="screenshot-12" width="410" height="609" srcset="https://codeandunicorns.com/wp-content/uploads/2017/02/screenshot-12-200x297.png 200w, https://codeandunicorns.com/wp-content/uploads/2017/02/screenshot-12-202x300.png 202w, https://codeandunicorns.com/wp-content/uploads/2017/02/screenshot-12-400x594.png 400w, https://codeandunicorns.com/wp-content/uploads/2017/02/screenshot-12-600x892.png 600w, https://codeandunicorns.com/wp-content/uploads/2017/02/screenshot-12-689x1024.png 689w, https://codeandunicorns.com/wp-content/uploads/2017/02/screenshot-12-768x1141.png 768w, https://codeandunicorns.com/wp-content/uploads/2017/02/screenshot-12-800x1189.png 800w, https://codeandunicorns.com/wp-content/uploads/2017/02/screenshot-12.png 1006w" sizes="(max-width: 410px) 100vw, 410px" /></a>
  
  <p class="wp-caption-text">
    Fig. 4 &#8211; Attaching the hello_world to a chart
  </p>
</div>

The _experts_ tab will be very useful later for when you wish to log events while the EA is chewing data, presenting results and even placing orders. To stop the EA you can right click on the chart &#8211; _**Expert Advisors > Remove**. _notice the EA name on the top right of the chart along with a smiley, you are sure to know your EA is working if this happens.

If you go through the [documentation](https://docs.mql4.com/) you&#8217;ll see there are plenty of things one can do with an EA. The MT4 api for accessing data is pretty interesting and allows the developers to try out trading strategies or collecting data for example. Before we finish lets lets take a step forward and write _EURUSD_  tick values to a file. I invite you to study the code below in case it&#8217;s not clear what it is supposed to do. You can add this snippet to the existing _hello_world OnTick_ function:

<pre class="brush: cpp; title: ; notranslate" title="">int file_handle = FileOpen("EURUSD", FILE_READ|FILE_WRITE|FILE_TXT|FILE_ANSI);

if(file_handle != INVALID_HANDLE) {
    if(FileSeek(file_handle, 0, SEEK_END)) {

        FileWriteString(file_handle, Symbol() + " - " + TimeCurrent() + " -&nbsp;Ask: " + Ask + "; Bid: " + Bid + "\n");
    }

}

FileClose(file_handle);
</pre>

So we open a file called &#8220;EURUSD&#8221;, make use of the integrated _INVALID_HANDLE_ constant to check for irregularities, if everything ok, get the end of the file and write _Tick_ data. The string format is merely illustrative.

If you ran the code above, on an &#8220;EURUSD&#8221; chart, soon enough you&#8217;ll have these tick lines being written on a file. If you go back to your _MetaEditor_, you&#8217;ll find the file &#8220;EURUSD&#8221; on your _files_ directory. If you have been paying attention, the fact we named the file &#8220;EURUSD&#8221; doesn&#8217;t really matter, you can attach this EA to any other chart and it will still work.

This simple example can be very useful if you wish to continue learning about MT4 and MQL4. Even if you are not fond of coding with MQL4 you can now use this data to test strategies on any other language before actually committing to having an EA executing on real-time data.

That&#8217;s it for today, I hope you find this information useful, feel free to let me know if you have any questions.

Further reading on MQL4:

  * [Difference between a script and an expert advisor](http://expert-advisor-builder.com/whats-the-difference-between-an-expert-advisor-and-an-mql-script/)
  * [Official MQL4 documentation](https://docs.mql4.com/)