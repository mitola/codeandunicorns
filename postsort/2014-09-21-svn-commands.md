---
id: 766
title: SVN commands listicle
date: 2014-09-21T18:48:38+00:00
author: Matjaz Trcek
layout: post
guid: http://codeandunicorns.com/?p=766
permalink: /svn-commands/
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
avada_post_views_count:
  - "2415"
sbg_selected_sidebar:
  - 'a:1:{i:0;s:1:"0";}'
sbg_selected_sidebar_replacement:
  - 'a:1:{i:0;s:12:"Blog Sidebar";}'
fusion_builder_content_backup:
  - |
    For everyone who have not yet transitioned to GIT from SVN I compiled my personal list that helps me with projects on which I need to use SVN versioning.
    
    &nbsp;
    <div><strong><span style="color: #000000;">Creating a branch from trunk: </span></strong>
    <div style="color: #000000;"></div>
    <div style="color: #000000;">svn cp trunk_URL branch_URL -m "Creating branch for ....."</div>
    <div style="color: #000000;"></div><p>
    <div style="color: #000000;"><strong>SVN merging:</strong></div><p>
    <div style="color: #000000;"></div>
    <div style="color: #000000;"></div>
    <div style="color: #000000;">cd to branch (with your command console), then user svn merge command while you are in the directory of the branch:</div>
    <div style="color: #000000;">
    <ul>
    <li>svn merge trunk_URL</li>
    </ul>
    </div>
    <div style="color: #000000;"></div>
    <div style="color: #000000;"></div>
    <div style="color: #000000;">
    <div>
    <div><strong>Basic commands:</strong></div>
    <div>
    <ul>
    <li>svn status //tells differences between original and to be committed version</li>
    <li>svn commit -m "Comment <span style="font-family: Helvetica;">“ //normal commit for svn</span></li>
    <li>svn ci -m "Fixed all those horrible crashes" foo bar baz graphics/logo.png   //commit only certain files<span style="font-family: Helvetica;">
    </span></li>
    <li>svn checkout https….branch_url</li>
    <li><span style="font-family: Helvetica;">svn add —force .     //Adding files to svn versioning. Beacuse of . the ignore files are handled correctly. use * to override</span></li>
    <li>svn status | grep "^!" | sed 's/^! *//g' | xargs svn rm   //removes files that were manually removed and also everything flagged with ! so be careful<span style="font-family: Helvetica;">
    </span></li>
    <li><span style="font-family: Helvetica;">svn log -l 3    // get last 3 commits</span></li>
    <li><span style="font-family: Helvetica;">svn log --verbose -r 26458 //details for revision 26458</span></li>
    <li>svn rm // branch delete<span style="font-family: Helvetica;">
    </span></li>
    <li>svn log --limit 15 --verbose branch_or_trunk_URL //shows last 15 commits with which files were changed</li>
    <li>svn merge --reintegrate branch_URL   trunk_URL //merging branch back to trunk</li>
    <li>svn revert --depth=infinity . //reverting folder back to last commit</li>
    </ul>
    </div>
    </div>
    </div>
    <div style="color: #000000;"><strong>Special commands:</strong></div>
    <div style="color: #000000;">See the log for a certain time range
    <ul>
    <li>svn log --revision {2014-01-20}:{2014-01-30}</li>
    </ul>
    Cherry-picking a revision and merging to trunk
    <ul>
    <li>svn merge -c revisionNumber branch_URL</li>
    </ul>
    Command used for resolving tree conflicts (There are always some :p )
    <ul>
    <li>svn resolve --accept working -R &lt;path&gt;</li>
    </ul>
    </div>
    <div style="color: #000000;"></div>
    </div>
fusion_builder_converted:
  - 'yes'
categories:
  - ALL
---
For everyone who have not yet transitioned to GIT from SVN I compiled my personal list that helps me with projects on which I need to use SVN versioning.

&nbsp;

<div>
  <strong><span style="color: #000000;">Creating a branch from trunk: </span></strong></p> 
  
  <div style="color: #000000;">
  </div>
  
  <div style="color: #000000;">
    svn cp trunk_URL branch_URL -m &#8220;Creating branch for &#8230;..&#8221;
  </div>
  
  <div style="color: #000000;">
  </div>
  
  <p>
    <div style="color: #000000;">
      <strong>SVN merging:</strong>
    </div>
    
    <p>
      <div style="color: #000000;">
      </div>
      
      <div style="color: #000000;">
      </div>
      
      <div style="color: #000000;">
        cd to branch (with your command console), then user svn merge command while you are in the directory of the branch:
      </div>
      
      <div style="color: #000000;">
        <ul>
          <li>
            svn merge trunk_URL
          </li>
        </ul>
      </div>
      
      <div style="color: #000000;">
      </div>
      
      <div style="color: #000000;">
      </div>
      
      <div style="color: #000000;">
        <div>
          <div>
            <strong>Basic commands:</strong>
          </div>
          
          <div>
            <ul>
              <li>
                svn status //tells differences between original and to be committed version
              </li>
              <li>
                svn commit -m &#8220;Comment <span style="font-family: Helvetica;">“ //normal commit for svn</span>
              </li>
              <li>
                svn ci -m &#8220;Fixed all those horrible crashes&#8221; foo bar baz graphics/logo.png   //commit only certain files<span style="font-family: Helvetica;"><br /> </span>
              </li>
              <li>
                svn checkout https….branch_url
              </li>
              <li>
                <span style="font-family: Helvetica;">svn add —force .     //Adding files to svn versioning. Beacuse of . the ignore files are handled correctly. use * to override</span>
              </li>
              <li>
                svn status | grep &#8220;^\!&#8221; | sed &#8216;s/^\! *//g&#8217; | xargs svn rm   //removes files that were manually removed and also everything flagged with ! so be careful<span style="font-family: Helvetica;"><br /> </span>
              </li>
              <li>
                <span style="font-family: Helvetica;">svn log -l 3    // get last 3 commits</span>
              </li>
              <li>
                <span style="font-family: Helvetica;">svn log &#8211;verbose -r 26458 //details for revision 26458</span>
              </li>
              <li>
                svn rm // branch delete<span style="font-family: Helvetica;"><br /> </span>
              </li>
              <li>
                svn log &#8211;limit 15 &#8211;verbose branch_or_trunk_URL //shows last 15 commits with which files were changed
              </li>
              <li>
                svn merge &#8211;reintegrate branch_URL   trunk_URL //merging branch back to trunk
              </li>
              <li>
                svn revert &#8211;depth=infinity . //reverting folder back to last commit
              </li>
            </ul>
          </div>
        </div>
      </div>
      
      <div style="color: #000000;">
        <strong>Special commands:</strong>
      </div>
      
      <div style="color: #000000;">
        See the log for a certain time range</p> 
        
        <ul>
          <li>
            svn log &#8211;revision {2014-01-20}:{2014-01-30}
          </li>
        </ul>
        
        <p>
          Cherry-picking a revision and merging to trunk
        </p>
        
        <ul>
          <li>
            svn merge -c revisionNumber branch_URL
          </li>
        </ul>
        
        <p>
          Command used for resolving tree conflicts (There are always some :p )
        </p>
        
        <ul>
          <li>
            svn resolve &#8211;accept working -R <path>
          </li>
        </ul>
      </div>
      
      <div style="color: #000000;">
      </div></div>