---
title: 'Get weekly CPU usage function &#8211; AWS Python Lambda'
date: 2018-08-23T15:25:35+00:00
author: Matjaz Trcek
layout: post
guid: https://codeandunicorns.com/?p=2509
permalink: /get-weekly-cpu-usage-function-aws-python-lambda/
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
pyre_slider_type:
  - 'no'
pyre_slider:
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
pyre_main_top_padding:
  - ""
pyre_main_bottom_padding:
  - ""
pyre_hundredp_padding:
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
pyre_sidebar_sticky:
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
pyre_page_title_line_height:
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
fusion_builder_status:
  - ""
kd_featured-image-2_post_id:
  - ""
kd_featured-image-3_post_id:
  - ""
kd_featured-image-4_post_id:
  - ""
kd_featured-image-5_post_id:
  - ""
avada_post_views_count:
  - "5735"
sbg_selected_sidebar:
  - 'a:1:{i:0;s:1:"0";}'
sbg_selected_sidebar_replacement:
  - 'a:1:{i:0;s:12:"Blog Sidebar";}'
sbg_selected_sidebar_2:
  - 'a:1:{i:0;s:1:"0";}'
sbg_selected_sidebar_2_replacement:
  - 'a:1:{i:0;s:0:"";}'
image: /wp-content/uploads/2018/08/lambdapython.png
categories:
  - ALL
  - How to
  - The Code
---
Let&#8217;s first cover the gist of the actual functionality that will be responsible for giving us averaged CPU utilization during a specific time frame. The code itself is a run of the mill kind of code but already coupled in a nice working example so quite easy adapted.

If we take a look at the function bellow&#8230;

<pre class="brush: python; title: ; notranslate" title="">import boto3
import sys
from datetime import datetime, timedelta

def get_cpu_util(instanceID,startTime,endTime):

        client = boto3.client('cloudwatch')
        response = client.get_metric_statistics(
            Namespace='AWS/EC2',
            MetricName='CPUUtilization',
            Dimensions=[
                {
                'Name': 'InstanceId',
                'Value': instanceID
                },
            ],
            
            StartTime=startTime,
            EndTime=endTime,
            Period=86400,
            Statistics=[
                'Average',
            ],
            Unit='Percent'
        )
        
        for k, v in response.items():
            if k == 'Datapoints':
                for y in v:
                    return "{0:.2f}".format(y['Average'])
</pre>

&#8230; We can see it accepts instanceID,startTime and endTime, which should optimally be of <a href="https://docs.python.org/2/library/datetime.html" target="_blank" rel="noopener">datetime</a> type format.  
In namespace we define AWS/EC2 but it can be also for example RDS etc. just check the AWS docs on the namespaces.

Other atributes should be quite selfexplanatory.

At the end there is a for loop that cycle&#8217;s through all data of the response and only returns the average time for the period.

One level higher we connect that function to connect it in a higher amount of instances (all of the instances inside the account) that get cycled through.

To get all of the instances with ID and only the ones that are running we need follow code for Python AWS lambda.

<pre class="brush: python; title: ; notranslate" title="">#get all instances
    instanceIDs=[]
    ec2 = boto3.resource('ec2')
    instances = ec2.instances.filter(
        Filters=[{'Name': 'instance-state-name', 'Values': ['running']}])
</pre>

With the following code we only get the running instances, and beacuse a lot of times you would also like to have human readable name of the instance we use the following code to get the name key tag.

<pre class="brush: python; title: ; notranslate" title="">for instance in instances:
        tmpDict=get_cpu_util(instance.id,startTime,endTime)
        if tmpDict:
            for tags in instance.tags:
                try:
                    if tags['Key'] == 'Name':
                      tmpDict['Name']=tags['Value']
                      break
                except KeyError: pass
            else:
                print("Name not found")
</pre>

A short and sweet Python combo, hopefully it is useful to someone