---
id: 1577
title: Antipatterns in software development
date: 2016-01-11T17:30:08+00:00
author: Matjaz Trcek
layout: post
guid: https://codeandunicorns.com/?p=1577
permalink: /antipatterns-software-development/
slide_template:
  - default
fusion_builder_status:
  - inactive
avada_post_views_count:
  - "4168"
dsq_thread_id:
  - "4482063554"
fusion_builder_content_backup:
  - |
    Recently I was diving deep into Antipatterns and found them terribly interesting. Here is a list of quite many different sourced possible antipatterns and their wag abound descriptions.
    <h3>Big ball of mud:</h3>
    Simple way of saying it: An apocalyptic mess. It lacks an understandable and coherent architecture, it can happen commonly due to big pressure, unsustainable growth and need to fix it fast and dirty to make it work, basically just hacking it together or hacking to make it work.
    <h3>Magic push-button:</h3>
    Antipattern connected with graphical user interface (GUI). Common in methodologies such as Waterfall where design and coding is separated, but it happens otherwise as well. It happens when the front end is inconsistent with the backend, as for example having one button on design and multiple steps in the coding part to be required from front end. A good way of avoiding it is having a designer/UX with coding experience.
    <h3>Race hazard:</h3>
    Failing to see the consequences or timings of instructions that can sometimes interfere with each other. An example of that would be when having two instructions of increasing a global counter by one after another in parallel without waiting for a previous instruction to finish. The result of increasing two times like that could happen to be 0+1+1(at the same time)=1.
    <h3>Stovepipe system:</h3>
    Also lots of times a legacy system. The meaning behind is that components are independent in a way, the code and common functionality doesn't get reused. In most cases that's a really bad thing, but in certain cases it is done on purpose, since you don't have dependencies on other parts of code.
    <h3>God object / The Blob</h3>
    The object of God or the God object is an object that really knows too much or can do to many things. Instead of separating functionality, problems, etc. into smaller pieces and classes, the god object is a big piece of code or even the whole program that is the opposite of separating the code into manageable pieces.
    
    I'm pretty sure most of us used this pattern at least once before on our learning curve...
    <h3>Continuous Obsolescence / perpetual revolution</h3>
    Technology is changing so rapidly that software developers need to invest a lot of work to learn them and finding other software that can work good in combinations. Specifically to this antipattern example is Nuke Dukem Forever which was continually rewritten with use of newer technologies delaying its release for a long time. Sufficient to mention it increased cost quite a bit.
    <h3>Lava Flow</h3>
    It's a problem of releasing solution still in development to production environment. Part of the problem can be adding backwards compatibility since pre-released system has now dependencies connected with it. And the other part of problem lies with the dead code, an example of which is when developers on the project change and thus part of the knowledge is lost. The subsequent developers can then either refactor or avoid the code and increase the complexity (latter being part of the lava flow antipattern).
    <h3>Ambiguous Viewpoint</h3>
    Object-oriented analysis and design  models are often presented without clarifying the viewpoint represented by the model. By default, this models denote an implementation viewpoint that is potentially the least useful. Mixed viewpoints don’t allow the fundamental separation of interfaces from implementation details, which is one of the primary benefits of the object-oriented paradigm.
    <h3>Functional Decomposition</h3>
    The functional decomposition antipattern usually occurs due to experienced developers who are coming from a structural language (Fortran, etc.) and trying to develop program in object-oriented language. The code can be very complex due to this as procedural developers have a different way of approaching and coding the problem.
    <h3>Poltergeists / Gypsy wagon</h3>
    The lovely clutterers of the object-oriented programming. They are usually intentional and made by inexperienced developers. They add extra steps to the design architecture with for example being a controller class connecting 10 different classes etc. That makes it more complicated even though simpler, more streamlined design can be used. And since they are needed they only take extra resources and are rarely used.
    <h3>Boat Anchor</h3>
    A Boat Anchor is a software or hardware which is usually bought but never really used on the project. Many times it can be part of the policy in the acquiring other software with getting an Anchor extra. But you can get it as well due to buying the software without technical review or discussion
    <h3>Golden Hammer</h3>
    Antipattern of a Golden Hammer is when same technology or a product is used as an universal solution.
    <h3>Dead End</h3>
    Dead End happens when changes are applied to a reusable piece of code or component that is no longer supported/maintained  from original supplier. When the changes are applied, the maintenance transfers to internal developers. Since the code is external the features and bug fixes are harder to integrate.
    <h3>Spaghetti Code</h3>
    Ad hoc software structure makes it difficult to extend and optimize code. Frequent code refactoring can improve software structure, support software maintenance, and enable iterative development.
    
    Another famous example. Spaghetti Code (Interestingly there is also Lasagna and Ravioli code, and just the thought makes me hungry...) is an ad hoc software structure that makes it incredibly difficult to extend and refactor code. The way to negate or improve it is with frequent refactoring and iterative development.
    <h3>Input Kludge</h3>
    Input Kludge is where simple user input is not handled correctly or handled at all. For example, if a computer program accepts text input from user, an ad hoc algorithm will mishandle many combinations input strings to legal or illegal combs.  They are usually hard to detect with unit tests but easily discovered by users.
    <h3>Walking through a Minefield/Nothing Works or Do You Believe in Magic?</h3>
    Using today’s software technology is analogous to walking through a high-tech mine field. Numerous bugs are found in released software products; in fact, experts estimate that original source code contains two to five bugs per line of code.
    
    It has multiple names, and it's simply awesome. Somehow it has so many bugs that if it was a minefield, you would probably not survive even few meters, but somehow, kinda, maybe works but not really. It is so bug abundant in released production software that it can contain more bugs than lines.
    <h3>Cut-and-Paste Programming</h3>
    Code reused by copying source statements leads to significant maintenance problems. Alternative forms of reuse, including black-box reuse, reduce maintenance issues by having common source code, testing, and documentation.
    <h3>Mushroom Management</h3>
    In some architecture and management circles, there is an explicit policy to keep system developers isolated from the system’s end users. Requirements are passed second-hand through intermediaries, including architects, managers, or requirements analysts.
    
    Having an amazing multilayered architecture and management. Separating the developers from end users and only passing requirements through managers,architects, business analysts, etc. The result of that is the end product can be significantly different to what user actually wanted. If the process is more iterative and connecting end-users and developers there can be a big cost reduction and efficiency gained.
    
    References:
    
    What are Development AntiPatterns? (2015) Anti-pattern[Online], 1 December 2015. Authors: William Brown, Raphael Malveau, Hays McCormick, Thomas Mowbray, and Scott W. Thomas. Available at: <a href="http://www.antipatterns.com/dev_cat.htm">http://www.antipatterns.com/dev_cat.htm</a>
    Sourcemaking (2015) Software Development AntiPatterns. Available at: <a href="https://sourcemaking.com/antipatterns/software-development-antipatterns">https://sourcemaking.com/antipatterns/software-development-antipatterns</a>
    Wikipedia (2015) Anti-pattern[Online], 1 December 2015. Available at: <a href="https://en.wikipedia.org/wiki/Anti-pattern">https://en.wikipedia.org/wiki/Anti-pattern</a>
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
categories:
  - ALL
  - News
  - Science
  - The Code
---
Recently I was diving deep into Antipatterns and found them terribly interesting. Here is a list of quite many different sourced possible antipatterns and their wag abound descriptions.

### Big ball of mud:

Simple way of saying it: An apocalyptic mess. It lacks an understandable and coherent architecture, it can happen commonly due to big pressure, unsustainable growth and need to fix it fast and dirty to make it work, basically just hacking it together or hacking to make it work.

### Magic push-button:

Antipattern connected with graphical user interface (GUI). Common in methodologies such as Waterfall where design and coding is separated, but it happens otherwise as well. It happens when the front end is inconsistent with the backend, as for example having one button on design and multiple steps in the coding part to be required from front end. A good way of avoiding it is having a designer/UX with coding experience.

### Race hazard:

Failing to see the consequences or timings of instructions that can sometimes interfere with each other. An example of that would be when having two instructions of increasing a global counter by one after another in parallel without waiting for a previous instruction to finish. The result of increasing two times like that could happen to be 0+1+1(at the same time)=1.

### Stovepipe system:

Also lots of times a legacy system. The meaning behind is that components are independent in a way, the code and common functionality doesn&#8217;t get reused. In most cases that&#8217;s a really bad thing, but in certain cases it is done on purpose, since you don&#8217;t have dependencies on other parts of code.

### God object / The Blob

The object of God or the God object is an object that really knows too much or can do to many things. Instead of separating functionality, problems, etc. into smaller pieces and classes, the god object is a big piece of code or even the whole program that is the opposite of separating the code into manageable pieces.

I&#8217;m pretty sure most of us used this pattern at least once before on our learning curve&#8230;

### Continuous Obsolescence / perpetual revolution

Technology is changing so rapidly that software developers need to invest a lot of work to learn them and finding other software that can work good in combinations. Specifically to this antipattern example is Nuke Dukem Forever which was continually rewritten with use of newer technologies delaying its release for a long time. Sufficient to mention it increased cost quite a bit.

### Lava Flow

It&#8217;s a problem of releasing solution still in development to production environment. Part of the problem can be adding backwards compatibility since pre-released system has now dependencies connected with it. And the other part of problem lies with the dead code, an example of which is when developers on the project change and thus part of the knowledge is lost. The subsequent developers can then either refactor or avoid the code and increase the complexity (latter being part of the lava flow antipattern).

### Ambiguous Viewpoint

Object-oriented analysis and design  models are often presented without clarifying the viewpoint represented by the model. By default, this models denote an implementation viewpoint that is potentially the least useful. Mixed viewpoints don’t allow the fundamental separation of interfaces from implementation details, which is one of the primary benefits of the object-oriented paradigm.

### Functional Decomposition

The functional decomposition antipattern usually occurs due to experienced developers who are coming from a structural language (Fortran, etc.) and trying to develop program in object-oriented language. The code can be very complex due to this as procedural developers have a different way of approaching and coding the problem.

### Poltergeists / Gypsy wagon

The lovely clutterers of the object-oriented programming. They are usually intentional and made by inexperienced developers. They add extra steps to the design architecture with for example being a controller class connecting 10 different classes etc. That makes it more complicated even though simpler, more streamlined design can be used. And since they are needed they only take extra resources and are rarely used.

### Boat Anchor

A Boat Anchor is a software or hardware which is usually bought but never really used on the project. Many times it can be part of the policy in the acquiring other software with getting an Anchor extra. But you can get it as well due to buying the software without technical review or discussion

### Golden Hammer

Antipattern of a Golden Hammer is when same technology or a product is used as an universal solution.

### Dead End

Dead End happens when changes are applied to a reusable piece of code or component that is no longer supported/maintained  from original supplier. When the changes are applied, the maintenance transfers to internal developers. Since the code is external the features and bug fixes are harder to integrate.

### Spaghetti Code

Ad hoc software structure makes it difficult to extend and optimize code. Frequent code refactoring can improve software structure, support software maintenance, and enable iterative development.

Another famous example. Spaghetti Code (Interestingly there is also Lasagna and Ravioli code, and just the thought makes me hungry&#8230;) is an ad hoc software structure that makes it incredibly difficult to extend and refactor code. The way to negate or improve it is with frequent refactoring and iterative development.

### Input Kludge

Input Kludge is where simple user input is not handled correctly or handled at all. For example, if a computer program accepts text input from user, an ad hoc algorithm will mishandle many combinations input strings to legal or illegal combs.  They are usually hard to detect with unit tests but easily discovered by users.

### Walking through a Minefield/Nothing Works or Do You Believe in Magic?

Using today’s software technology is analogous to walking through a high-tech mine field. Numerous bugs are found in released software products; in fact, experts estimate that original source code contains two to five bugs per line of code.

It has multiple names, and it&#8217;s simply awesome. Somehow it has so many bugs that if it was a minefield, you would probably not survive even few meters, but somehow, kinda, maybe works but not really. It is so bug abundant in released production software that it can contain more bugs than lines.

### Cut-and-Paste Programming

Code reused by copying source statements leads to significant maintenance problems. Alternative forms of reuse, including black-box reuse, reduce maintenance issues by having common source code, testing, and documentation.

### Mushroom Management

In some architecture and management circles, there is an explicit policy to keep system developers isolated from the system’s end users. Requirements are passed second-hand through intermediaries, including architects, managers, or requirements analysts.

Having an amazing multilayered architecture and management. Separating the developers from end users and only passing requirements through managers,architects, business analysts, etc. The result of that is the end product can be significantly different to what user actually wanted. If the process is more iterative and connecting end-users and developers there can be a big cost reduction and efficiency gained.

References:

What are Development AntiPatterns? (2015) Anti-pattern

<div  class="fusion-fullwidth fullwidth-box hundred-percent-fullwidth"  style='background-color: #ffffff;background-position: center center;background-repeat: no-repeat;padding-top:0px;padding-right:0px;padding-bottom:0px;padding-left:0px;'>
  <div class="fusion-builder-row fusion-row ">
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        [Online], 1 December 2015. Authors: William Brown, Raphael Malveau, Hays McCormick, Thomas Mowbray, and Scott W. Thomas. Available at: <a href="http://www.antipatterns.com/dev_cat.htm">http://www.antipatterns.com/dev_cat.htm</a><br /> Sourcemaking (2015) Software Development AntiPatterns. Available at: <a href="https://sourcemaking.com/antipatterns/software-development-antipatterns">https://sourcemaking.com/antipatterns/software-development-antipatterns</a><br /> Wikipedia (2015) Anti-pattern[Online], 1 December 2015. Available at: <a href="https://en.wikipedia.org/wiki/Anti-pattern">https://en.wikipedia.org/wiki/Anti-pattern</a>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
  </div>
</div>