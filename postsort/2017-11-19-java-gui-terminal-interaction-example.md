---
id: 2324
title: Java GUI terminal interaction example
date: 2017-11-19T13:24:08+00:00
author: Matjaz Trcek
layout: post
guid: https://codeandunicorns.com/?p=2324
permalink: /java-gui-terminal-interaction-example/
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
  - "10346"
sbg_selected_sidebar:
  - 'a:1:{i:0;s:1:"0";}'
sbg_selected_sidebar_replacement:
  - 'a:1:{i:0;s:12:"Blog Sidebar";}'
sbg_selected_sidebar_2:
  - 'a:1:{i:0;s:1:"0";}'
sbg_selected_sidebar_2_replacement:
  - 'a:1:{i:0;s:0:"";}'
dsq_thread_id:
  - "6294865564"
image: /wp-content/uploads/2017/11/tab2_commands-min.png
categories:
  - ALL
  - How to
  - The Code
---
The following example will go over following Github repo created specifically for this.

**Github: **

<https://github.com/mitola/selftomator>

It was primarily aimed to provide a bit of exploration space since I was looking at several ways to automate a couple of my workflows, so I explored through Java, Node.JS, terminal solutions etc.

In the current iteration of the project certain things are already prepared. The main class, that calls the form which is made out of 2 tabbed windows. On one there is a textPanel, TextInput and a Button.

<img class="aligncenter size-full wp-image-2331" src="https://codeandunicorns.com/wp-content/uploads/2017/11/tab1_console-min.png" alt="" width="1112" height="722" srcset="https://codeandunicorns.com/wp-content/uploads/2017/11/tab1_console-min-200x130.png 200w, https://codeandunicorns.com/wp-content/uploads/2017/11/tab1_console-min-300x195.png 300w, https://codeandunicorns.com/wp-content/uploads/2017/11/tab1_console-min-400x260.png 400w, https://codeandunicorns.com/wp-content/uploads/2017/11/tab1_console-min-600x390.png 600w, https://codeandunicorns.com/wp-content/uploads/2017/11/tab1_console-min-768x499.png 768w, https://codeandunicorns.com/wp-content/uploads/2017/11/tab1_console-min-800x519.png 800w, https://codeandunicorns.com/wp-content/uploads/2017/11/tab1_console-min-1024x665.png 1024w, https://codeandunicorns.com/wp-content/uploads/2017/11/tab1_console-min.png 1112w" sizes="(max-width: 1112px) 100vw, 1112px" /> 

On the other one, as you can see on the featured post it&#8217;s where you can save command&#8217;s that will launch their local consoles (which are cmd on Windows, OS X terminal on Mac and equivalent on Linux) . Currently consisting of TextInput&#8217;s and Buttons with a label. All the GUI is done with the inbuilt IntelliJ From Builder for Java. The console launching functionality is quite a stub ATM. But at least basic examples I found are attached in the commentary of the code itself.

Now let&#8217;s focus on the actual fun part.

## Code:

<pre class="brush: java; title: ; notranslate" title="">public class Main {
    public static void main(String[] args) {
        JFrame frame = new JFrame("Console interaction");
        frame.setContentPane(new MainApp().panelMain);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.pack();
        frame.setVisible(true);
    }
}
</pre>

In the main class we first instantiate a new [JFrame](https://docs.oracle.com/javase/7/docs/api/javax/swing/JFrame.html) titled Console interaction.  
For the frame itself we connect the other main class which contains direct references to the form etc. Of the new class we connect driectly to panelMain.  
PanelMain is the root of the GUI form, on which everything else is attached. The frame object itself contains loads of other useful config which I didn&#8217;t utilise but feel free to do it with one of existing setters. To create for example a fixed width and height on it.

Now lets take a close look at MainApp class. I&#8217;ll be adding just the relevant snippets of code in here, and the rest can be seen on above mentioned Github URL.

<pre class="brush: java; title: ; notranslate" title="">public class MainApp {
    public JPanel panelMain;
    private JTextField msg;
    private JTextPane consoleOutput;
    private JButton msgSend;
    private JTabbedPane mainTabber;
    private JScrollPane scrollConsoleWrapper;
    private JTextField cmd1;
    private JButton cmd1b;
    private JTextField cmd2;
    private JTextField cmd3;
    private JTextField cmd4;
    private JButton cmd2b;
    private JButton cmd3b;
    private JButton cmd4b;
</pre>

This are all the GUI elements placed on MainApp.form file. It doesn&#8217;t make much sense to show MainApp.form code since it&#8217;s very XML-ish look alike, and we can use GUI builder for it anyway.

<pre class="brush: java; title: ; notranslate" title="">ConsoleIntegration console = new ConsoleIntegration();
      try {
          loadPropertiesProperty();
      } catch (IOException e) {
          e.printStackTrace();
      }
</pre>

We will be using this variables later on to connect listeners and other kind of functionality to it.  
In public MainApp function we first instantiate a helper class ConsoleIntegration which contains methods related to native consoles.

<pre class="brush: java; title: ; notranslate" title="">msgSend.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                String consoleCommand = msg.getText();
                try {
                   consoleOutput.setText(consoleOutput.getText() + console.consoleExecOutput(consoleCommand));
                } catch (IOException e1) {
                    e1.printStackTrace();
                } catch (InterruptedException e1) {
                    e1.printStackTrace();
                }
            }
        });
</pre>

On button that is showed on the last image where you can input a console command and have a button next to it. We attached listener to it. That listener will take the value of the text input (msg.getText()) and execute it in the consoleExecOutput which sends it to native console and outputs whatever the console outputs. An example would be sending a common &#8220;ls&#8221; command that will return the file names of the current pointed to directory.

The output will get appended to the TextArea panel, where outputs of previous commands will rest as well. Everything is made scrollable with wrapper of ScrollPane surrounding the TextArea.

Now we will momentarily jump into ConsoleIntegration consoleExecOutput to see what the method even does.

<pre class="brush: java; title: ; notranslate" title="">public String consoleExecOutput(String inputCommand) throws IOException, InterruptedException {
        String consoleOutput="";

        Process proc = Runtime.getRuntime().exec(inputCommand);

        // Read the output

        BufferedReader reader =
                new BufferedReader(new InputStreamReader(proc.getInputStream()));

        String line = "";
        while((line = reader.readLine()) != null) {
            System.out.print(line + "\n");
            consoleOutput=consoleOutput+line + "\n";
        }

        proc.waitFor();

        return consoleOutput;
    }
</pre>

In this function as you can see the inputCommand is taken, proc Process executed with command and the [BufferedReader](https://docs.oracle.com/javase/7/docs/api/java/io/BufferedReader.html) collects the output itself. since the output can be more then one line we wait until all output is collected and combine it together and return back to the main class where it gets outputted to textPane.

That&#8217;s pretty much it for the first tab, some thing&#8217;s of course don&#8217;t work yet, such as canceling the input with CTRL+C, and other things which would need to be done custom.

But since it&#8217;s just a demo and a bit of practice, the code itself isn&#8217;t up to par anyway, but hopefully it will help with some ideas etc.

Lets take a look at second tab now which contains 4 input fields and buttons.

<pre class="brush: java; title: ; notranslate" title="">cmd1.addFocusListener(new FocusAdapter() {
            @Override
            public void focusLost(FocusEvent e) {
                savePropertySet(1);
                super.focusLost(e);
            }
        });
        cmd2.addFocusListener(new FocusAdapter() {
            @Override
            public void focusLost(FocusEvent e) {
                savePropertySet(2);
                super.focusLost(e);
            }
        });
        cmd3.addFocusListener(new FocusAdapter() {
            @Override
            public void focusLost(FocusEvent e) {
                savePropertySet(3);
                super.focusLost(e);
            }
        });
        cmd4.addFocusListener(new FocusAdapter() {
            @Override
            public void focusLost(FocusEvent e) {
                savePropertySet(4);
                super.focusLost(e);
            }
        });
</pre>

So in this case I improvised a bit and set when the text field losses focus, it executes the function to save the input in a local property.dat file.  
The thinking about this simplified interaction is, that if you want to change and edit the command for later, you will lose focus sooner or later, either hovering out, tabbing, etc.

<pre class="brush: java; title: ; notranslate" title="">static void saveProperties(Properties p)throws IOException
    {
        FileWriter fw = new FileWriter("property.dat",true); //the true will append the new data
        p.store(fw,"properties");
        fw.close();
        System.out.println("After saving properties:"+p);
    }
</pre>

In the function itself. we take the properties defined before from the text input and save it in property.dat file. Since it&#8217;s connected lets take a look at loadProperties as well, which gets loaded on program startup.

<pre class="brush: java; title: ; notranslate" title="">void loadPropertiesProperty()throws IOException
    {
        Properties p = new Properties();

        FileInputStream fi=new FileInputStream("property.dat");
        p.load(fi);
        fi.close();

        cmd1.setText(p.getProperty("cmd1"));
        cmd2.setText(p.getProperty("cmd2"));
        cmd3.setText(p.getProperty("cmd3"));
        cmd4.setText(p.getProperty("cmd4"));
        System.out.println("After Loading properties:"+p);
    }
</pre>

Of course it&#8217;s not a good practice at all to write in this kind of un-modular un logical way, but it provides a quick way of prototyping to just confirm some propositions i had, and didn&#8217;t focus on program architecture itself. In the function we open the property.dat file and get appropriate properties via getProperty and set it in appropariate textInput field.

If you take a look at openTerminalWithCommand function in ConsoleIntegration class it&#8217;s just a stub of the code, but that provides some hints on adding appropriate ways of starting native consoles.

<pre class="brush: java; title: ; notranslate" title="">public void openTerminalWithCommand(String inputCommand){
        String nameOS = System.getProperty("os.name");

        System.out.println(nameOS);

        if (nameOS.startsWith("Windows")){
            //// windows only
        /*Process p = Runtime.getRuntime().exec("cmd /c start cmd.exe");
        p.waitFor();*/
        } else if (nameOS.startsWith("Mac")){
            //Mac
        /*
        Runtime.getRuntime().exec("/usr/bin/open -a Terminal /path/to/the/executable");
         */

        } else if (nameOS.startsWith("Linux")){
            //Linux      // GNU/Linux -- example

            //Runtime.getRuntime().exec("/usr/bin/x-terminal-emulator --disable-factory -e cat README.txt");

        }
    }
}
</pre>

And for the end, don&#8217;t forget you can just clone the repo and take a closer look into it on **Github**:  
<https://github.com/mitola/selftomator>