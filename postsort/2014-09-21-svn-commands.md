---
title: SVN commands listicle
date: 2014-09-21T18:48:38+00:00
author: Matjaz Trcek
layout: post
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