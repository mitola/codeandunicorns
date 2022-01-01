---
id: 1400
title: Sublime build systems and Mocha.js
date: 2015-10-04T17:08:52+00:00
author: Joao Pereira
layout: post
guid: https://codeandunicorns.com/?p=1400
permalink: /sublime-build-and-mocha/
slide_template:
  - default
fusion_builder_status:
  - inactive
avada_post_views_count:
  - "3601"
dsq_thread_id:
  - "4193253520"
fusion_builder_content_backup:
  - |
    Keeping your projects well organised and tested can bring some cool benefits besides the obvious often referred in the books. One I am really fond of is defining a uniform test structure in par with the source code. Something simple like:
    <blockquote>root
    |-src/index.js
    |-test/index_test.js</blockquote>
    .. and then adapt my Sublime editor to run my <strong>Mocha.js</strong> tests for the file I am currently working on. This is no big news and you can find documentation around the web in order to do it.
    <blockquote>...<strong>Atom</strong> already provides a better context test runner!</blockquote>
    That might be true, but with little extra work you can make <strong>Sublime</strong> outperform <strong>Atom</strong> easily. To do that we need to add a <strong>build system</strong>.
    <h3>Setting everything up</h3>
    To start off you need to navigate to <strong>Tools</strong>-<strong>Build System</strong>-<strong>New Build System...</strong>. A new tab will open and now we are ready to start our configuration. Here's a basic <strong>build system</strong>:
    
    [code]
    {
    &quot;cmd&quot;: [&quot;mocha&quot;],
    &quot;working_dir&quot;: &quot;${project_path:${folder}}&quot;
    }
    [/code]
    
    As you can see it's nothing more than a JSON file with some configurations. The <strong>cmd</strong> property is the command it will be run on the specified <strong>working_dir</strong>. Neat right? You can use this for pretty much anything: running tests, running deployment scripts, git commands and so forth.
    
    So how can we wrap up a nice build system to run the specific tests of the file we are currently working on? To do that we need to understand some other features <strong>Sublime</strong> offers us. We can add to our previous <strong>build system</strong> the following:
    
    [code]
    {
    &quot;cmd&quot;: [&quot;mocha&quot;, &quot;${file}&quot;],
    &quot;working_dir&quot;: &quot;${project_path:${folder}}&quot;
    }
    [/code]
    
    This will now run mocha on the the current file opened in the editor.
    
    We are getting there but we are not quite there yet. Imagine we are working on <strong>src/index.js</strong> and we want to run the tests related to our file which are located in <strong>test/index_test.js</strong>. We need a way to relate our files but in fact that's already done, notice we can use the pattern <strong>filename_test.js</strong> to do that. As such we can create a small script file with the commands we want to run via <strong>Sublime</strong>, instead of just running them directly from the <strong>build system</strong>.
    
    I'll just go ahead and present a simple <strong>makefile</strong> which will do that for us:
    
    [code language="bash"]
    test:
    ifeq ($(findstring _test.js,$(REPORTER_FILE)),_test.js)
    @mocha --bail $(REPORTER)
    else
    @find test -name $(subst .js,_test.js,$(REPORTER_FILE)) | xargs mocha
    endif
    
    .PHONY: test
    [/code]
    
    As you can see we have a simple conditional checking what type file we reported back to the <strong>makefile</strong>. If the file contains already our test pattern, run <strong>mocha</strong> directly on it (the --bail flag is optional, it just stops testing if one of the test fails). Otherwise find our test files and run <strong>mocha</strong> on it.
    
    Finally we adapt our <strong>build system</strong>:
    
    [code]
    {
    &quot;cmd&quot;: [&quot;make&quot;, &quot;REPORTER=${file}&quot;, &quot;REPORTER_FILE=${file_name}&quot;],
    &quot;working_dir&quot;: &quot;${project_path:${folder}}&quot;
    }
    [/code]
    
    And <strong>BAM</strong> with just a <strong>CMD + B</strong> the console panel will come up on <strong>Sublime</strong> and run the tests related to your current working file.
    <h3>More tricks</h3>
    The great thing about keeping a build like this is that there's even more you can do with <strong>Mocha</strong>. For example you can create a pattern on each test file for a specific test to run and use the <strong>--grep</strong> option from <strong>Mocha</strong> to run tests matching that pattern instead of running all tests in the file. Or go even deeper by using <strong>--fgrep</strong> and only run the tests matching a specific string.
    
    These are all tips for being a bit more productive and an extra reason for everyone to make the world a better place and try <strong>Test Driven Development</strong>. There's nothing more comfortable than developing with a nicely organized test suite!
    
    Enjoy!
    
    <strong>NOTE:</strong> If for some reason your node modules are not tied to your <strong>$PATH</strong> you can also add another property to your <strong>build system</strong> called "path": "path_here".
    <h3>References:</h3>
    <h4>1 - <a href="http://docs.sublimetext.info/en/latest/reference/build_systems.html?highlight=build%20system">Sublime build systems</a></h4>
    <h4>2 - <a href="https://github.com/accerqueira/sublime-test-runner">Sublime test runner</a></h4>
    <h4>3 - <a href="https://mochajs.org">Mocha js</a></h4>
fusion_builder_converted:
  - 'yes'
sbg_selected_sidebar:
  - 'a:1:{i:0;s:1:"0";}'
sbg_selected_sidebar_replacement:
  - 'a:1:{i:0;s:12:"main_sidebar";}'
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
image: /wp-content/uploads/2015/10/4561741727_067ba817bb_b.jpg
categories:
  - ALL
---
Keeping your projects well organised and tested can bring some cool benefits besides the obvious often referred in the books. One I am really fond of is defining a uniform test structure in par with the source code. Something simple like:

> root  
> |-src/index.js  
> |-test/index_test.js

.. and then adapt my Sublime editor to run my **Mocha.js** tests for the file I am currently working on. This is no big news and you can find documentation around the web in order to do it.

> &#8230;**Atom** already provides a better context test runner!

That might be true, but with little extra work you can make **Sublime** outperform **Atom** easily. To do that we need to add a **build system**.

### Setting everything up

To start off you need to navigate to **Tools**&#8211;**Build System**&#8211;**New Build System&#8230;**. A new tab will open and now we are ready to start our configuration. Here&#8217;s a basic **build system**:

<div  class="fusion-fullwidth fullwidth-box hundred-percent-fullwidth"  style='background-color: #ffffff;background-position: center center;background-repeat: no-repeat;padding-top:0px;padding-right:0px;padding-bottom:0px;padding-left:0px;'>
  <div class="fusion-builder-row fusion-row ">
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: plain; title: ; notranslate" title="">
{
  "cmd": ["mocha"],
  "working_dir": "${project_path:${folder}}"
}
</pre>
        
        <p>
          As you can see it&#8217;s nothing more than a JSON file with some configurations. The <strong>cmd</strong> property is the command it will be run on the specified <strong>working_dir</strong>. Neat right? You can use this for pretty much anything: running tests, running deployment scripts, git commands and so forth.
        </p>
        
        <p>
          So how can we wrap up a nice build system to run the specific tests of the file we are currently working on? To do that we need to understand some other features <strong>Sublime</strong> offers us. We can add to our previous <strong>build system</strong> the following:
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: plain; title: ; notranslate" title="">
{
  "cmd": ["mocha", "${file}"],
  "working_dir": "${project_path:${folder}}"
}
</pre>
        
        <p>
          This will now run mocha on the the current file opened in the editor.
        </p>
        
        <p>
          We are getting there but we are not quite there yet. Imagine we are working on <strong>src/index.js</strong> and we want to run the tests related to our file which are located in <strong>test/index_test.js</strong>. We need a way to relate our files but in fact that&#8217;s already done, notice we can use the pattern <strong>filename_test.js</strong> to do that. As such we can create a small script file with the commands we want to run via <strong>Sublime</strong>, instead of just running them directly from the <strong>build system</strong>.
        </p>
        
        <p>
          I&#8217;ll just go ahead and present a simple <strong>makefile</strong> which will do that for us:
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: bash; title: ; notranslate" title="">
test:
ifeq ($(findstring _test.js,$(REPORTER_FILE)),_test.js)
	@mocha --bail $(REPORTER)
else
	@find test -name $(subst .js,_test.js,$(REPORTER_FILE)) | xargs mocha
endif

.PHONY: test
</pre>
        
        <p>
          As you can see we have a simple conditional checking what type file we reported back to the <strong>makefile</strong>. If the file contains already our test pattern, run <strong>mocha</strong> directly on it (the &#8211;bail flag is optional, it just stops testing if one of the test fails). Otherwise find our test files and run <strong>mocha</strong> on it.
        </p>
        
        <p>
          Finally we adapt our <strong>build system</strong>:
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: plain; title: ; notranslate" title="">
{
  "cmd": ["make", "REPORTER=${file}", "REPORTER_FILE=${file_name}"],
  "working_dir": "${project_path:${folder}}"
}
</pre>
        
        <p>
          And <strong>BAM</strong> with just a <strong>CMD + B</strong> the console panel will come up on <strong>Sublime</strong> and run the tests related to your current working file.
        </p>
        
        <h3>
          More tricks
        </h3>
        
        <p>
          The great thing about keeping a build like this is that there&#8217;s even more you can do with <strong>Mocha</strong>. For example you can create a pattern on each test file for a specific test to run and use the <strong>&#8211;grep</strong> option from <strong>Mocha</strong> to run tests matching that pattern instead of running all tests in the file. Or go even deeper by using <strong>&#8211;fgrep</strong> and only run the tests matching a specific string.
        </p>
        
        <p>
          These are all tips for being a bit more productive and an extra reason for everyone to make the world a better place and try <strong>Test Driven Development</strong>. There&#8217;s nothing more comfortable than developing with a nicely organized test suite!
        </p>
        
        <p>
          Enjoy!
        </p>
        
        <p>
          <strong>NOTE:</strong> If for some reason your node modules are not tied to your <strong>$PATH</strong> you can also add another property to your <strong>build system</strong> called &#8220;path&#8221;: &#8220;path_here&#8221;.
        </p>
        
        <h3>
          References:
        </h3>
        
        <h4>
          1 &#8211; <a href="http://docs.sublimetext.info/en/latest/reference/build_systems.html?highlight=build%20system">Sublime build systems</a>
        </h4>
        
        <h4>
          2 &#8211; <a href="https://github.com/accerqueira/sublime-test-runner">Sublime test runner</a>
        </h4>
        
        <h4>
          3 &#8211; <a href="https://mochajs.org">Mocha js</a>
        </h4>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
  </div>
</div>