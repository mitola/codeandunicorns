---
id: 780
title: Simple broad web crawler with Java
date: 2014-10-12T13:45:56+00:00
author: Matjaz Trcek
layout: post
guid: http://codeandunicorns.com/?p=780
permalink: /simple-broad-web-crawler-java/
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
  - "5747"
sbg_selected_sidebar:
  - 'a:1:{i:0;s:1:"0";}'
sbg_selected_sidebar_replacement:
  - 'a:1:{i:0;s:12:"Blog Sidebar";}'
fusion_builder_content_backup:
  - |
    The following article is a a very simple presentation with examples and explanation regarding the web crawler I made in Java. The idea behind it was to make <strong>portable</strong> (Java+Sqllite - No install needed for DB) and <strong>simple</strong> (The program was not designed to be scalable, be multithreaded, store a lot of data about the site or make a clever ranking, but it was rather aimed as a very simple working indexed &amp; webcrawler).
    
    &nbsp;
    <h3>Fell free to fork or modify the source code without restrictions. Mentioned author or link to the website is welcome:</h3>
    <ul>
    <li>
    <h3><strong><a href="https://github.com/mitola/BroadWebCrawlerIndexer">Source code is available on Github</a></strong></h3>
    </li>
    </ul>
    <h3>You will also need:</h3>
    <ul>
    <li>
    <h3><a href="http://jsoup.org/">Jsoup</a></h3>
    </li>
    <li>
    <h3><a href="http://www.sqlite.org/">sqllite</a></h3>
    </li>
    </ul>
    &nbsp;
    
    I'll try to explain the whole logic, so let's just start on the main function.
    The main function initializes database class and through the constructor creates necessary tables if they are not yet created. After that it continues into method executionOfMenuChoice()
    
    [code lang="java"]
    public static void main(String[] args) throws Exception {
    //init DB interaction
    try {
    dbClass = new MainDBClass();
    } catch (Exception ex) {
    Logger.getLogger(WebCrawler.class.getName()).log(Level.SEVERE, null, ex);
    }
    
    //Init menu  choice and execution
    executionOfMenuChoice();
    }
    [/code]
    
    From the main function it continues to infinite loop of this function which first displays the menu and prepares reading of user input. The comments in each case should be self explanatory.
    
    [code lang="java"]
    public static void executionOfMenuChoice() throws Exception {
    while (true) {
    menuView();
    Scanner in = new Scanner(System.in);
    String input = in.next();
    switch (input) {
    case &quot;1&quot;:
    //process through all of the links on a page and continue
    String[] nextEntryForProcessing;
    while (true) {
    nextEntryForProcessing = dbClass.getNextEntryForProcessing();
    urlParsing(nextEntryForProcessing[0]); //0 is url and 1 is title
    dbClass.moveEntryAfterParsing(nextEntryForProcessing[0], nextEntryForProcessing[1]);
    }
    case &quot;2&quot;:
    //use this method to get all the results plus number of rows on the end for each table
    dbClass.getAllEntriesCollected();
    break;
    case &quot;3&quot;:
    dbClass.getAllEntriesCollectedCount();
    break;
    case &quot;4&quot;:
    //Use truncate if you wish to delete your tables
    dbClass.truncateTables();
    break;
    case &quot;5&quot;:
    //Exiting an application
    System.exit(0);
    }
    }
    }
    [/code]
    
    Function menuview called from executionOfMenuChoice, just a simple console menu...
    
    [code lang="java"]
    public static void menuView() throws Exception {
    System.out.println(&quot;############################&quot;);
    System.out.println(&quot;1.) Press 1 to start/continue parsing and collecting links and titles&quot;);
    System.out.println(&quot;2.) Press 2 to print all collected and parsed links&quot;);
    System.out.println(&quot;3.) Press 3 to print number of processed and collected links&quot;);
    System.out.println(&quot;4.) Press 4 to truncate all data in the tables&quot;);
    System.out.println(&quot;4.) Press 5 to exit&quot;);
    System.out.println(&quot;############################&quot;);
    }
    [/code]
    
    And the first thing that happens in main method while constructing the DB class. First it defines globally conn variable which is used for handling db connection and after that it continues into creation od DB if content didn't exist before.
    
    [code lang="java"]
    public MainDBClass() throws Exception {
    Class.forName(&quot;org.sqlite.JDBC&quot;);
    this.conn = DriverManager.getConnection(&quot;jdbc:sqlite:linkdatabase.db&quot;);
    createTables();
    }
    [/code]
    
    And in the createTable function on the last line, I added the first entry which will be used as a starting point for the parser.
    
    [code lang="java"]
    public void createTables() throws Exception{
    Statement stat = conn.createStatement();
    
    stat.executeUpdate(&quot;CREATE TABLE IF NOT EXISTS collected_links (url TEXT UNIQUE, title);&quot;);
    stat.executeUpdate(&quot;CREATE TABLE IF NOT EXISTS processed_links (url TEXT UNIQUE, title);&quot;);
    stat.executeUpdate(&quot;INSERT OR IGNORE INTO collected_links VALUES('http://codeandunicorns.com', 'Dummy link');&quot;);
    }
    [/code]
    
    Ok, the basic part of the web crawler is finished. we initialised everything and prepared it for use.
    Let's return to executionOfMenuChoice function and follow the case 1. It goes into infinite loop and cycles through the lines below:
    
    [code lang="java"]
    nextEntryForProcessing = dbClass.getNextEntryForProcessing();
    urlParsing(nextEntryForProcessing[0]); //0 is url and 1 is title
    dbClass.moveEntryAfterParsing(nextEntryForProcessing[0], nextEntryForProcessing[1]);
    [/code]
    
    In the first line dbClass.getNextEntryForProcessing it gets the next entry from table of collected_links, processes/parse it in the second line and moves it to processed_links table in third line.
    
    Let us take a closer look at the most important part for a web crawler which is urlParsing function which continues into processPage function.
    
    [code lang="java"]
    public static void processPage(String URL) throws Exception {
    //get useful information
    boolean skip = false;
    Document doc = null;
    try {
    doc = Jsoup.connect(URL).timeout(5 * 1000).ignoreContentType(true).get();
    } catch (IOException ex) {
    Logger.getLogger(WebCrawler.class.getName()).log(Level.SEVERE, null, ex);
    dbClass.moveEntryAfterParsing(URL, URL);
    skip = true;
    }
    
    //get all links and recursively call the processPage method
    if (!skip) {
    Elements questions = doc.select(&quot;a[href]&quot;);
    for (Element link : questions) {
    
    //inserts every new url into DB
    if (link.attr(&quot;abs:href&quot;).startsWith(&quot;http&quot;)) {
    System.out.println(link.attr(&quot;abs:href&quot;));
    /*Document titleDoc = Jsoup.connect(URL).get();
    String title = doc.title();*/
    if (!link.attr(&quot;abs:href&quot;).contains(&quot; &quot;)) {
    dbClass.insertNewEntry(link.attr(&quot;abs:href&quot;), link.attr(&quot;abs:href&quot;));
    }
    }
    }
    }
    }
    [/code]
    
    First we use Jsoup.connect with timeout parameter which increases the effectivnes of parser since some websites can be quite slow. We also use ignoreContentType since it helps ignoring false positives for urls.
    After that we use the seen code snippet that extracts all the href links from a website and saves them in collected_links table where they wait to be used processed again and put into processed_links.
    <h2></h2>
fusion_builder_converted:
  - 'yes'
categories:
  - How to
  - The Code
---
The following article is a a very simple presentation with examples and explanation regarding the web crawler I made in Java. The idea behind it was to make **portable** (Java+Sqllite &#8211; No install needed for DB) and **simple** (The program was not designed to be scalable, be multithreaded, store a lot of data about the site or make a clever ranking, but it was rather aimed as a very simple working indexed & webcrawler).

&nbsp;

### Fell free to fork or modify the source code without restrictions. Mentioned author or link to the website is welcome:

  * ### **[Source code is available on Github](https://github.com/mitola/BroadWebCrawlerIndexer)**

### You will also need:

  * ### [Jsoup](http://jsoup.org/)

  * ### [sqllite](http://www.sqlite.org/)

&nbsp;

I&#8217;ll try to explain the whole logic, so let&#8217;s just start on the main function.  
The main function initializes database class and through the constructor creates necessary tables if they are not yet created. After that it continues into method executionOfMenuChoice()

<div  class="fusion-fullwidth fullwidth-box hundred-percent-fullwidth"  style='background-color: #ffffff;background-position: center center;background-repeat: no-repeat;padding-top:0px;padding-right:0px;padding-bottom:0px;padding-left:0px;'>
  <div class="fusion-builder-row fusion-row ">
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: java; title: ; notranslate" title="">
    public static void main(String[] args) throws Exception {
        //init DB interaction
        try {
            dbClass = new MainDBClass();
        } catch (Exception ex) {
            Logger.getLogger(WebCrawler.class.getName()).log(Level.SEVERE, null, ex);
        }

        //Init menu  choice and execution
        executionOfMenuChoice();
    }
</pre>
        
        <p>
          From the main function it continues to infinite loop of this function which first displays the menu and prepares reading of user input. The comments in each case should be self explanatory.
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: java; title: ; notranslate" title="">
    public static void executionOfMenuChoice() throws Exception {
        while (true) {
            menuView();
            Scanner in = new Scanner(System.in);
            String input = in.next();
            switch (input) {
                case "1":
                    //process through all of the links on a page and continue
                    String[] nextEntryForProcessing;
                    while (true) {
                        nextEntryForProcessing = dbClass.getNextEntryForProcessing();
                        urlParsing(nextEntryForProcessing[0]); //0 is url and 1 is title
                        dbClass.moveEntryAfterParsing(nextEntryForProcessing[0], nextEntryForProcessing[1]);
                    }
                case "2":
                    //use this method to get all the results plus number of rows on the end for each table
                    dbClass.getAllEntriesCollected();
                    break;
                case "3":
                    dbClass.getAllEntriesCollectedCount();
                    break;
                case "4":
                    //Use truncate if you wish to delete your tables
                    dbClass.truncateTables();
                    break;
                case "5":
                    //Exiting an application
                    System.exit(0);
            }
        }
    }
</pre>
        
        <p>
          Function menuview called from executionOfMenuChoice, just a simple console menu&#8230;
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: java; title: ; notranslate" title="">
    public static void menuView() throws Exception {
        System.out.println("############################");
        System.out.println("1.) Press 1 to start/continue parsing and collecting links and titles");
        System.out.println("2.) Press 2 to print all collected and parsed links");
        System.out.println("3.) Press 3 to print number of processed and collected links");
        System.out.println("4.) Press 4 to truncate all data in the tables");
        System.out.println("4.) Press 5 to exit");
        System.out.println("############################");
    }
</pre>
        
        <p>
          And the first thing that happens in main method while constructing the DB class. First it defines globally conn variable which is used for handling db connection and after that it continues into creation od DB if content didn&#8217;t exist before.
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: java; title: ; notranslate" title="">
    public MainDBClass() throws Exception {
        Class.forName("org.sqlite.JDBC");
        this.conn = DriverManager.getConnection("jdbc:sqlite:linkdatabase.db");
        createTables();
    }
</pre>
        
        <p>
          And in the createTable function on the last line, I added the first entry which will be used as a starting point for the parser.
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: java; title: ; notranslate" title="">
    public void createTables() throws Exception{
        Statement stat = conn.createStatement();

        stat.executeUpdate("CREATE TABLE IF NOT EXISTS collected_links (url TEXT UNIQUE, title);");
        stat.executeUpdate("CREATE TABLE IF NOT EXISTS processed_links (url TEXT UNIQUE, title);");
        stat.executeUpdate("INSERT OR IGNORE INTO collected_links VALUES('http://codeandunicorns.com', 'Dummy link');");
    }
</pre>
        
        <p>
          Ok, the basic part of the web crawler is finished. we initialised everything and prepared it for use.<br /> Let&#8217;s return to executionOfMenuChoice function and follow the case 1. It goes into infinite loop and cycles through the lines below:
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: java; title: ; notranslate" title="">
    nextEntryForProcessing = dbClass.getNextEntryForProcessing();
    urlParsing(nextEntryForProcessing[0]); //0 is url and 1 is title
    dbClass.moveEntryAfterParsing(nextEntryForProcessing[0], nextEntryForProcessing[1]);
</pre>
        
        <p>
          In the first line dbClass.getNextEntryForProcessing it gets the next entry from table of collected_links, processes/parse it in the second line and moves it to processed_links table in third line.
        </p>
        
        <p>
          Let us take a closer look at the most important part for a web crawler which is urlParsing function which continues into processPage function.
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: java; title: ; notranslate" title="">
   public static void processPage(String URL) throws Exception {
        //get useful information
        boolean skip = false;
        Document doc = null;
        try {
            doc = Jsoup.connect(URL).timeout(5 * 1000).ignoreContentType(true).get();
        } catch (IOException ex) {
            Logger.getLogger(WebCrawler.class.getName()).log(Level.SEVERE, null, ex);
            dbClass.moveEntryAfterParsing(URL, URL);
            skip = true;
        }

        //get all links and recursively call the processPage method
        if (!skip) {
            Elements questions = doc.select("a[href]");
            for (Element link : questions) {

                //inserts every new url into DB
                if (link.attr("abs:href").startsWith("http")) {
                    System.out.println(link.attr("abs:href"));
                    /*Document titleDoc = Jsoup.connect(URL).get();
                     String title = doc.title();*/
                    if (!link.attr("abs:href").contains(" ")) {
                        dbClass.insertNewEntry(link.attr("abs:href"), link.attr("abs:href"));
                    }
                }
            }
        }
    }
</pre>
        
        <p>
          First we use Jsoup.connect with timeout parameter which increases the effectivnes of parser since some websites can be quite slow. We also use ignoreContentType since it helps ignoring false positives for urls.<br /> After that we use the seen code snippet that extracts all the href links from a website and saves them in collected_links table where they wait to be used processed again and put into processed_links.
        </p>
        
        <h2>
        </h2>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
  </div>
</div>