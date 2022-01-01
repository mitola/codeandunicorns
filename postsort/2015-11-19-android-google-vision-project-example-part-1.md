---
id: 1451
title: Android Google Vision project example part 1
date: 2015-11-19T15:47:36+00:00
author: Matjaz Trcek
layout: post
guid: https://codeandunicorns.com/?p=1451
permalink: /android-google-vision-project-example-part-1/
slide_template:
  - default
fusion_builder_status:
  - inactive
avada_post_views_count:
  - "5142"
fusion_builder_content:
  - ""
dsq_thread_id:
  - "4333245085"
fusion_builder_content_backup:
  - |
    <a href="https://codeandunicorns.com/wp-content/uploads/2015/11/GoogleVisionMatjazAPI2.jpg"><img src="https://codeandunicorns.com/wp-content/uploads/2015/11/GoogleVisionMatjazAPI2-177x300.jpg" alt="GoogleVisionMatjazAPI2" width="177" height="300" class="alignleft size-medium wp-image-1509" /></a>The following article is an example of using Google Vision API which was recently released by Google. The Vision API is capable of detecting smiles, winks and multiple faces in the picture, as well as providing multiple reference points from which you can define and use your own programmable detections and behaviours. In the following example the smile probability is used together with displaying the camera live feed, detecting face/faces and displaying a preview.
    
    Based on the smile probability it will either provide you with a joke or a quote, which will further be synthesized with a TTS (text to speech API).
    
    P.S. The article will be split into multiple parts so it will be easier to read and digest the content. On the last page of article, you also have a Github repo where the source code is hosted.
    
    P.S.S. Code is partially accompanied with text and partially with in-line comments for clearer understanding.
    
    Variable initialisation in MainActivity:
    
    [code lang="java"]
    private static final String TAG = &quot;FaceTracker&quot;;
    
    private CameraSource mCameraSource;
    private CameraSourcePreview mPreview;
    private GraphicOverlay mGraphicOverlay;
    private ImageView mImageView;
    private TextView mJokeView;
    private TextToSpeech mTts;
    private static final int CAMERA_REQUEST = 1888;
    private float smileValue = 1.0f;
    private String[] jokes; //jokes array, at the moment hardcoded but in the future there could be a much better solution, just meant as a sample for now
    private String[] quotes; //same here
    [/code]
    
    Ok now lets move to OnCreate. I will ignore the common parts that are always used in general in Android and try to focus in most part on things related to this project.
    OnCreate function definition:
    <a href="https://codeandunicorns.com/wp-content/uploads/2015/11/GoogleVisionMatjazAPIDemo.jpg"><img src="https://codeandunicorns.com/wp-content/uploads/2015/11/GoogleVisionMatjazAPIDemo-175x300.jpg" alt="GoogleVisionMatjazAPIDemo" width="175" height="300" class="alignright size-medium wp-image-1508" /></a>
    First we start with init of main parts as for example Admob view, if you want to monetize, i just wanted to include this as an extra. Then init of all relevant things, as mPreviw(used for previewing the camera on screen), mGraphic overlay (which is used for overlaying face preview with either the box,dots,any values you want etc.), and init of FaceDetector which helps us detect the face features such as smiling blinking and if needed around I think 24 common points of the face to detect custom features.
    
    [code lang="java"]
    public void onCreate(Bundle icicle) {
    super.onCreate(icicle);
    setContentView(R.layout.activity_main);
    
    AdView mAdView = (AdView) findViewById(R.id.adView);
    AdRequest adRequest = new AdRequest.Builder().build();
    mAdView.loadAd(adRequest);
    
    mPreview = (CameraSourcePreview) findViewById(R.id.preview);
    mGraphicOverlay = (GraphicOverlay) findViewById(R.id.faceOverlay);
    mImageView = (ImageView) findViewById(R.id.imageView);
    mJokeView = (TextView) findViewById(R.id.jokeView);
    mImageView.setVisibility(View.INVISIBLE);
    
    Context context = getApplicationContext();
    FaceDetector detector = new FaceDetector.Builder(context)
    .setClassificationType(FaceDetector.ALL_CLASSIFICATIONS)
    .setProminentFaceOnly(true)
    .build();
    detector.setProcessor(
    new MultiProcessor.Builder&amp;lt;&amp;gt;(new GraphicFaceTrackerFactory()).build());
    
    
    if (!detector.isOperational()) {
    // Note: The first time that an app using face API is installed on a device, GMS will
    // download a native library to the device in order to do detection.  Usually this
    // completes before the app is run for the first time.  But if that download has not yet
    // completed, then the above call will not detect any faces.
    //
    // isOperational() can be used to check if the required native library is currently
    // available.  The detector will automatically become operational once the library
    // download completes on device.
    Log.w(TAG, &quot;Face detector dependencies are not yet available.&quot;);
    }
    [/code]
    
    With continue with init of Camera, with settings of preview resolutoin, which camera to use, FPS speed etc, we also init TTS(Google's text to speech system which we use in combination with our Google Vision API)
    
    [code lang="java"]
    mCameraSource = new CameraSource.Builder(context, detector)
    .setRequestedPreviewSize(640, 480)
    .setFacing(CameraSource.CAMERA_FACING_FRONT)
    .setRequestedFps(30.0f)
    .build();
    mTts = new TextToSpeech(MainActivity.this, new TextToSpeech.OnInitListener(){
    @Override
    public void onInit(int status) {
    // TODO Auto-generated method stub
    if(status == TextToSpeech.SUCCESS){
    int result=mTts.setLanguage(Locale.US);
    if(result==TextToSpeech.LANG_MISSING_DATA ||
    result==TextToSpeech.LANG_NOT_SUPPORTED){
    Log.e(&quot;error&quot;, &quot;This Language is not supported&quot;);
    }
    else{
    if (android.os.Build.VERSION.SDK_INT&amp;gt;=21){
    mTts.speak(&quot;Welcome to: Do you smile?&quot;, TextToSpeech.QUEUE_ADD, null, &quot;ss&quot;); //based on text, it gets transformed to voice of Google woman
    mTts.speak(&quot;Scan your current mood! Do you smile or not is the question?nClick and find out!&quot;, TextToSpeech.QUEUE_ADD, null, &quot;ss&quot;);
    }
    else{
    mTts.speak(&quot;Welcome to: Do you smile?&quot;, TextToSpeech.QUEUE_ADD, null);
    mTts.speak(&quot;Scan your current mood! Do you smile or not is the question?nClick and find out!&quot;, TextToSpeech.QUEUE_ADD, null);
    }
    }
    }
    else
    Log.e(&quot;error&quot;, &quot;Initilization Failed!&quot;);
    }
    });
    
    Button button =  (Button) findViewById(R.id.takepicturebutton); //take mood picture
    button.setOnClickListener(new View.OnClickListener() {
    public void onClick(View v) {
    mImageView.setVisibility(View.INVISIBLE);
    mPreview.takeImage(); // take image function together with later main processing part.
    }
    });
    
    //Main init of sample data
    initJokeStrings();
    initInspiriStrings();
    
    }
    [/code]
    
    Several smaller relevant methods, mostly for pausing,restarting, and clearing the memory of device with some minor management:
    
    [code lang="java"]
    /**
    * Restarts the camera.
    */
    @Override
    protected void onResume() {
    super.onResume();
    startCameraSource();
    }
    
    /**
    * Stops the camera.
    */
    @Override
    protected void onPause() {
    super.onPause();
    mPreview.stop();
    }
    
    /**
    * Releases the resources associated with the camera source, the associated detector, and the
    * rest of the processing pipeline.
    */
    @Override
    protected void onDestroy() {
    super.onDestroy();
    mCameraSource.release();
    }
    
    //==============================================================================================
    // Camera Source Preview
    //==============================================================================================
    
    /**
    * Starts or restarts the camera source, if it exists.  If the camera source doesn't exist yet
    * (e.g., because onResume was called before the camera source was created), this will be called
    * again when the camera source is created.
    */
    private void startCameraSource() {
    try {
    mPreview.start(mCameraSource, mGraphicOverlay);
    } catch (IOException e) {
    Log.e(TAG, &quot;Unable to start camera source.&quot;, e);
    mCameraSource.release();
    mCameraSource = null;
    }
    }
    [/code]
    
    Graphic face tracker initialization part:
    
    In this part we have some interesting methods for further investigation.
    One of them is setImageViewPicture. I know mostly it's simple but the interesting part is the
    
    [code lang="java"]
    mImageView.setImageBitmap(BitmapFactory.decodeByteArray(data, 0, data.length));
    [/code]
    
    line. Since it uses the provided byte data and decodes it to an imageView. After that it goes to either get inspirational quote or get random joke, depending on the float value of your smile determined in a later covered function and class.
    
    The second part of this code initializes its own instance for every face in the picture, but for our demo we are only utilizing the first and most prominent face.
    
    [code lang="java"]
    //==============================================================================================
    // Graphic Face Tracker
    //==============================================================================================
    
    /**
    * Factory for creating a face tracker to be associated with a new face.  The multiprocessor
    * uses this factory to create face trackers as needed -- one for each individual.
    */
    private class GraphicFaceTrackerFactory implements MultiProcessor.Factory&amp;lt;Face&amp;gt; {
    @Override
    public Tracker&amp;lt;Face&amp;gt; create(Face face) {
    return new GraphicFaceTracker(mGraphicOverlay);
    }
    }
    
    public void setImageViewPicture(final byte[] data){
    mImageView.setVisibility(View.VISIBLE);
    mImageView.setImageBitmap(BitmapFactory.decodeByteArray(data, 0, data.length));
    if(smileValue &amp;gt;= 0.50f){
    getInspirationalQoute(); // You are smiling
    }
    else{
    getRandomJoke(); //You do not smile
    }
    }
    
    /**
    * Face tracker for each detected individual. This maintains a face graphic within the app's
    * associated face overlay.
    */
    private class GraphicFaceTracker extends Tracker&amp;lt;Face&amp;gt; {
    private GraphicOverlay mOverlay;
    private FaceGraphic mFaceGraphic;
    
    GraphicFaceTracker(GraphicOverlay overlay) {
    mOverlay = overlay;
    mFaceGraphic = new FaceGraphic(overlay);
    }
    
    /**
    * Start tracking the detected face instance within the face overlay.
    */
    @Override
    public void onNewItem(int faceId, Face item) {
    mFaceGraphic.setId(faceId);
    }
    
    /**
    * Update the position/characteristics of the face within the overlay.
    */
    @Override
    public void onUpdate(FaceDetector.Detections&amp;lt;Face&amp;gt; detectionResults, Face face) {
    mOverlay.add(mFaceGraphic);
    mFaceGraphic.updateFace(face);
    smileValue = mFaceGraphic.getSmileProbability();
    }
    
    /**
    * Hide the graphic when the corresponding face was not detected.  This can happen for
    * intermediate frames temporarily (e.g., if the face was momentarily blocked from
    * view).
    */
    @Override
    public void onMissing(FaceDetector.Detections&amp;lt;Face&amp;gt; detectionResults) {
    mOverlay.remove(mFaceGraphic);
    }
    
    /**
    * Called when the face is assumed to be gone for good. Remove the graphic annotation from
    * the overlay.
    */
    @Override
    public void onDone() {
    mOverlay.remove(mFaceGraphic);
    }
    }
    [/code]
    
    The fun part with jokes and qoutes:
    
    Based as seen before on Smile probability from Google Vision API we can now go to for example a getRandomJoke function. Here we first check if the Android version is bigger then 21 or smaller, since based on the version i noticed then can sometimes be problemds due to one version of TTS speak function getting deprecated in newer versions, thats why I am separating both of them. It also accesses the string arrays and picks up random string value of quote or joke, to try to make you happy if you are sad, or just make you wiser if you smile enough already.
    
    [code lang="java"]
    public void getRandomJoke(){
    if (android.os.Build.VERSION.SDK_INT&amp;gt;=21){
    String joke = jokes[new Random().nextInt(jokes.length)];
    mTts.speak(joke, TextToSpeech.QUEUE_FLUSH, null, &quot;ss&quot;);
    mJokeView.setText(&quot;Joke, cause you don't smile:&quot; + &quot;n&quot; + joke);
    }
    else{
    mTts.speak(jokes[new Random().nextInt(jokes.length)], TextToSpeech.QUEUE_FLUSH, null);
    }
    }
    
    public void getInspirationalQoute() {
    if (android.os.Build.VERSION.SDK_INT&amp;gt;=21){
    String quote = quotes[new Random().nextInt(quotes.length)];
    mTts.speak(quote, TextToSpeech.QUEUE_FLUSH, null, &quot;ss&quot;);
    mJokeView.setText(&quot;Quote, cause you smile:&quot; + &quot;n&quot; + quote);
    }
    else{
    mTts.speak(quotes[new Random().nextInt(quotes.length)], TextToSpeech.QUEUE_FLUSH, null);
    }
    }
    [/code]
    
    Just for the sake of complete code the not so fine done array of jokes and qoutes.
    
    [code lang="java"]
    public void initJokeStrings(){
    jokes = new String[] {
    &quot;The clear history button in your browser has saved more lives than Superman&quot;,
    &quot;I bet earth makes fun of the other planets for having no life&quot;,
    &quot;Oh no! Playstation and Xbox online services are down! Someone call an ambulance! Wii U Wii U Wii U.&quot;,
    &quot;The sight of a woman's cleavage reduces a man's ability to think clearly by 50%... per boob!&quot;,
    &quot;Jimmy has 42 candy bars. Jimmy eats 24. What does jimmy have now? Diabetes.. Jimmy has diabetes.&quot;,
    &quot;What type of Bee's make milk instead of honey? Boobies&quot;,
    &quot;I gave my number to a really hot girl at the bar and told her to text me when she got home. She must be homeless&quot;,
    &quot;Just changed my Facebook name to ‘No one' so when I see stupid posts I can click like and it will say ‘No one likes this'.&quot;,
    &quot;What's the difference between snowmen and snowladies? Snowballs&quot;,
    &quot;How do you make holy water? You boil the hell out of it.&quot;,
    &quot;If con is the opposite of pro, it must mean Congress is the opposite of progress?&quot;,
    &quot;I wondered why the frisbee was getting bigger, and then it hit me.&quot;,
    &quot;I used to like my neighbors, until they put a password on their Wi-Fi.&quot;,
    &quot;Never argue with a fool, they will lower you to their level, and then beat you with experience.&quot;,
    &quot;Why do farts smell? So deaf people can enjoy them too.&quot;,
    &quot;Light travels faster than sound. This is why some people appear bright until they speak.&quot;,
    &quot;What did the ocean say to the beach? Nothing, it just waved.&quot;,
    &quot;I say no to alcohol, it just doesn't listen.&quot;,
    &quot;Why did the skeleton go to the party alone? -- He had no body to go with him!&quot;,
    &quot;Right now I'm having amnesia and deja vu at the same time! I think I've forgotten this before?&quot;,
    &quot;Why is Peter Pan always flying? Because he Neverlands.&quot;,
    &quot;I think i want a job cleaning mirrors, It's just something i could really see myself doing&quot;,
    &quot;My girlfriend keeps going on bout the time i jokingly put superglue on her mobile phone, honestly , she just can't let it go.&quot;,
    &quot;How do you make a tissue dance? You put a little boogie in it.&quot;,
    &quot;For Christmas, I want Santa's list of naughty girls.&quot;,
    &quot;Who says nothing is impossible. I've been doing nothing for years.&quot;
    };
    }
    
    public void initInspiriStrings(){
    quotes = new String[] {
    &quot;Things may come to those who wait, but only the things left by those who hustle. By Abraham Lincoln&quot;,
    &quot;The great secret of education is to direct vanity to proper objects. By Adam Smith&quot;,
    &quot;It’s not that travel just broadens your mind, rather it enables you to see how narrow your oppressor’s minds are. By Alain de Botton&quot;,
    &quot;A person who never made a mistake never tried anything new. By Alan Watts&quot;,
    &quot;Better to have a short life that is full of what you like doing than a long life spent in a miserable way. By Alan Watts&quot;,
    &quot;Life is a musical thing and you are supposed to dance and sign while it's being played. By Alan Watts&quot;,
    &quot;Omnipotence is not knowing how everything is done; it's just doing it. By Alan Watts&quot;,
    &quot;It is not humiliating to be unhappy. Physical suffering is sometimes humiliating, but the suffering of being cannot be, it is life. By Albert Camus&quot;,
    &quot;Learn from yesterday, live for today, hope for tomorrow. The important thing is not to stop questioning. By Albert Einstein&quot;,
    &quot;The secret to creativity is knowing how to hide your sources. By Albert Einstein&quot;,
    &quot;The true sign of intelligence is not knowledge but imagination. By Albert Einstein&quot;,
    &quot;The world as we have created it is a process of our thinking. It cannot be changed without changing our thinking. By Albert Einstein&quot;,
    &quot;When facts don't fit the theory, change the facts. By Albert Einstein&quot;,
    &quot;Creativity never comes under emotional stress or tension. The real creativity comes when the mind finally relaxes and is quiet and then can focus. By Amar Bose&quot;,
    &quot;If you think something is impossible, don't disturb the person doing it. By Amar Bose&quot;,
    &quot;If you want to build a ship, don't drum up people to collect wood and don't assign them tasks and work, but rather teach them to long for the endless immensity of the sea. By Antoine de Saint-Exupery&quot;,
    &quot;To love is not to look at one another: it is to look, together, in the same direction. By Antoine de Saint-Exupery&quot;,
    &quot;When you give yourself, you receive more than you give. By Antoine de Saint-Exupery&quot;,
    &quot;Do not fear to be eccentric in opinion, for every opinion now accepted was once eccentric. By Bertrand Russell&quot;,
    &quot;Visionaries not only believe that the impossible can be done, but that it must be done. By Bran Ferren&quot;,
    &quot;People who have a strong sense of love and belonging believe they're worthy of it. By Brene Brown&quot;,
    &quot;Every human being has some flavor of ‘not enough.’ You can either be stopped by it, or simply notice it, like the weather. By Brigid Schulte&quot;,
    &quot;Anyone can complain about the world, but only a good few can fix it. By Cennydd Bowles&quot;,
    &quot;So many people rush through life, let's take our time living it. By Christian Vuerings&quot;,
    &quot;The more that you read, the more things you will know. The more that you learn, the more places you’ll go. By Doctor Seuss&quot;,
    &quot;Dichotomy between sense of wonder and what is wrong. By Elon Musk&quot;,
    &quot;If something is important enough, you should try. Even if the probable outcome is failure. By Elon Musk&quot;,
    &quot;There's skepticism about anything new. That's normal. By Elon Musk&quot;,
    &quot;There is only one way to happiness and that is to cease worrying about things which are beyond the power of our will. By Epictetus&quot;,
    &quot;There are 2 ways to make a man richer, give him more money or curb his desires. By Jean-Jacques Rousseau&quot;,
    &quot;Being deeply loved by someone gives you strength, while loving someone deeply gives you courage. By Lao Tse&quot;,
    &quot;A leader is best when people barely know he exists, when his work is done, his aim fulfilled, they will say: we did it ourselves. By Lao Tse&quot;,
    &quot;Silence is a source of great strength. By Lao Tse&quot;,
    &quot;To attain knowledge, add things every day. To attain wisdom, remove things every day. By Lao Tse&quot;,
    &quot;The best way to have a good idea is to have lots of ideas. By Linus Pauling&quot;,
    &quot;At home I am a nice guy: but I don't want the world to know. Humble people, I've found, don't get very far. By Muhammad Ali&quot;,
    &quot;He who is not courageous enough to take risks will accomplish nothing in life. By Muhammad Ali&quot;,
    &quot;I am the greatest, I said that even before I knew I was. By Muhammad Ali&quot;,
    &quot;It isn't the mountains ahead to climb that wear you out; it's the pebble in your shoe. By Muhammad Ali&quot;,
    &quot;The man who has no imagination has no wings. By Muhammad Ali&quot;,
    &quot;If there is no struggle, there is no progress. By Frederick Douglass&quot;,
    &quot;Success is a state of being. Because as soon as you say you're successful, you probably start to fail. By Howard H. Stevenson&quot;,
    &quot;The reasonable man adapts himself to the world; the unreasonable one persists in trying to adapt the world to himself. Therefore, all progress depends on the unreasonable man. By George Bernard Shaw&quot;,
    &quot;Life would be much easier to understand if mother nature gave us the source code. By Graeme MacWilliam&quot;,
    &quot;Coming together is a beginning; keeping together is progress; staying together is success. By Henry Ford&quot;,
    &quot;An ounce of experience is better than a ton of theory simply. By John Dewey&quot;,
    &quot;A journey of a thousand miles begins with a single step. By Laozi&quot;,
    &quot;A man is but the product of his thoughts what he thinks, he becomes. By Mahatma Gandhi&quot;,
    &quot;An ounce of practice is worth more than tons of preaching. By Mahatma Gandhi&quot;,
    &quot;Live as if you were to die tomorrow. Learn as if you were to live forever. By Mahatma Gandhi&quot;,
    &quot;You must be the change you wish to see in the world. By Mahatma Gandhi&quot;,
    &quot;You must be the change you wish to see in the world. By Mahatma Gandhi&quot;,
    &quot;I have never let my schooling interfere with my education. By Mark Twain&quot;,
    &quot;Never let the future disturb you. You will meet it, if you have to, with the same weapons of reason which today arm you against the present. By &quot;,
    &quot;Never believe that a few caring people can't change the world. For, indeed, that's all who ever have. By &quot;,
    &quot;Keep away from those who try to belittle your ambitions. Small people always do that, but the really great make you believe that you too can become great. By &quot;,
    &quot;Life is short, break the rules. By &quot;,
    &quot;A gentleman is one who never hurts anyone's feelings unintentionally. By Oscar Wilde&quot;,
    &quot;A man who does not think for himself does not think at all. By Oscar Wilde&quot;,
    &quot;Always forgive your enemies - nothing annoys them so much. By Oscar Wilde&quot;,
    &quot;America is the only country that went from barbarism to decadence without civilization in between. By Oscar Wilde&quot;,
    &quot;Between men and women there is no friendship possible. There is passion, enmity, worship, love, but no friendship. By Oscar Wilde&quot;,
    &quot;Education is an admirable thing, but it is well to remember from time to time that nothing that is worth knowing can be taught. By Oscar Wilde&quot;,
    &quot;Experience is simply the name we give our mistakes. By Oscar Wilde&quot;,
    &quot;If you want to tell people the truth, make them laugh, otherwise they’ll kill you. By Oscar Wilde&quot;,
    &quot;There are only two tragedies in life: one is not getting what one wants, and the other is getting it. By Oscar Wilde&quot;,
    &quot;Work is the curse of the drinking classes. By Oscar Wilde&quot;,
    &quot;If you’re far enough ahead that people can’t figure out if you’re joking, you know you’ve innovated. By Paul Buchheit&quot;,
    &quot;The first thing I do on day one is build something useful, then just keep improving it. By Paul Buchheit&quot;,
    &quot;Go where you’re celebrated, not where you’re tolerated. By Paul F. Davis&quot;,
    &quot;Maintain your spirit of curiosity, keep questioning things, and you’ll find new ways to innovate. By Richard Brandson&quot;,
    &quot;If I look confused it is because I am thinking. By Samuel Goldwyn&quot;,
    &quot;The harder I work, the luckier I get. By Samuel Goldwyn&quot;,
    &quot;When someone does a good job, applaud; it makes two people happy. By Samuel Goldwyn&quot;,
    &quot;Defenseless is the best choice for those seeking to grow. By Seth Godin&quot;,
    &quot;Ship often. Ship lousy stuff, but ship. Ship constantly. By Seth Godin&quot;,
    &quot;If you do something and it turns out pretty good, then you should go do something else wonderful, not dwell on it for too long. Just figure out what’s next. By Steve Jobs&quot;,
    &quot;Do not go where the path may lead, go instead where there is no path and leave a trail. By Ralph Waldo Emerson&quot;,
    &quot;For every minute you remain angry, you give up sixty seconds of peace of mind. By Ralph Waldo Emerson&quot;,
    &quot;Nothing great was ever achieved without enthusiasm. By Ralph Waldo Emerson&quot;,
    &quot;If you’re not a embarrassed by the first version of your product, you launched to late. By Reid Hoffman&quot;,
    &quot;You earn trust by providing innovative, quality products and keeping your word. By Richard Brandson&quot;,
    &quot;Nothing comes to a sleeper but a dream. By Richard Williams&quot;,
    &quot;While we teach, we learn. By Seneca The Younger&quot;,
    &quot;Being the richest man in the cemetery doesn’t matter to me … Going to bed at night saying we’ve done something wonderful… that’s what matters to me. By Steve Jobs&quot;,
    &quot;One must learn by doing the thing; for though you think you know it, you have no certainty until you try. By Sophocles&quot;,
    &quot;The enemy of sustainable productivity is not stress. Rather, it’s the absence of intermittent rest and renewal. By Tony Schwartz&quot;,
    &quot;I keep going anyway. I pause and take the doubts in. I cry. I curse. I think it's unfair and that I can't continue. But then I do. I get up, brush my shoulders off, and carry on. By Tiffany Han&quot;,
    &quot;A man is not idle because he is absorbed in thought. There is a visible labor and there is an invisible labor. By Victor Hugo&quot;,
    &quot;He who opens a school door, closes a prison. By Victor Hugo&quot;,
    &quot;Initiative is doing the right thing without being told. By Victor Hugo&quot;,
    &quot;There is nothing more powerful than an idea whose time has come. By Victor Hugo&quot;,
    &quot;When a woman is talking to you, listen to what she says with her eyes. By Victor Hugo&quot;,
    &quot;Being male is a matter of birth. Being a man is a matter of age. But being a Gentleman is a matter of choice. By Vin Diesel&quot;,
    &quot;Education shouldn't fill a bucket but light a fire. By William Butler Yeats&quot;,
    &quot;There are no strangers here; Only friends you haven't yet met. By William Butler Yeats&quot;,
    };
    }
    [/code]
    
    [button link="https://codeandunicorns.com/android-google-vision-api-project-example-part-2" color="blue" size="large" type="flat" shape="round" target="_self" title="" gradient_colors="|" gradient_hover_colors="|" accent_color="" accent_hover_color="" bevel_color="" border_width="1px" icon="" icon_divider="yes" icon_position="right" modal="" animation_type="0" animation_direction="down" animation_speed="0.1" alignment="center" class="" id=""]Go to part 2[/button]
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
  - How to
  - Science
  - The Code
---
[<img class="alignleft size-medium wp-image-1509" src="https://codeandunicorns.com/wp-content/uploads/2015/11/GoogleVisionMatjazAPI2-177x300.jpg" alt="GoogleVisionMatjazAPI2" width="177" height="300" srcset="https://codeandunicorns.com/wp-content/uploads/2015/11/GoogleVisionMatjazAPI2-177x300.jpg 177w, https://codeandunicorns.com/wp-content/uploads/2015/11/GoogleVisionMatjazAPI2.jpg 463w" sizes="(max-width: 177px) 100vw, 177px" />](https://codeandunicorns.com/wp-content/uploads/2015/11/GoogleVisionMatjazAPI2.jpg)The following article is an example of using Google Vision API which was recently released by Google. The Vision API is capable of detecting smiles, winks and multiple faces in the picture, as well as providing multiple reference points from which you can define and use your own programmable detections and behaviours. In the following example the smile probability is used together with displaying the camera live feed, detecting face/faces and displaying a preview.

Based on the smile probability it will either provide you with a joke or a quote, which will further be synthesized with a TTS (text to speech API).

P.S. The article will be split into multiple parts so it will be easier to read and digest the content. On the last page of article, you also have a Github repo where the source code is hosted.

P.S.S. Code is partially accompanied with text and partially with in-line comments for clearer understanding.

Variable initialisation in MainActivity:

<div  class="fusion-fullwidth fullwidth-box hundred-percent-fullwidth"  style='background-color: #ffffff;background-position: center center;background-repeat: no-repeat;padding-top:0px;padding-right:0px;padding-bottom:0px;padding-left:0px;'>
  <div class="fusion-builder-row fusion-row ">
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: java; title: ; notranslate" title="">   
    private static final String TAG = "FaceTracker";

    private CameraSource mCameraSource;
    private CameraSourcePreview mPreview;
    private GraphicOverlay mGraphicOverlay;
    private ImageView mImageView;
    private TextView mJokeView;
    private TextToSpeech mTts;
    private static final int CAMERA_REQUEST = 1888;
    private float smileValue = 1.0f;
    private String[] jokes; //jokes array, at the moment hardcoded but in the future there could be a much better solution, just meant as a sample for now
    private String[] quotes; //same here
</pre>
        
        <p>
          Ok now lets move to OnCreate. I will ignore the common parts that are always used in general in Android and try to focus in most part on things related to this project.<br /> OnCreate function definition:<br /> <a href="https://codeandunicorns.com/wp-content/uploads/2015/11/GoogleVisionMatjazAPIDemo.jpg"><img class="alignright size-medium wp-image-1508" src="https://codeandunicorns.com/wp-content/uploads/2015/11/GoogleVisionMatjazAPIDemo-175x300.jpg" alt="GoogleVisionMatjazAPIDemo" width="175" height="300" srcset="https://codeandunicorns.com/wp-content/uploads/2015/11/GoogleVisionMatjazAPIDemo-175x300.jpg 175w, https://codeandunicorns.com/wp-content/uploads/2015/11/GoogleVisionMatjazAPIDemo.jpg 459w" sizes="(max-width: 175px) 100vw, 175px" /></a><br /> First we start with init of main parts as for example Admob view, if you want to monetize, i just wanted to include this as an extra. Then init of all relevant things, as mPreviw(used for previewing the camera on screen), mGraphic overlay (which is used for overlaying face preview with either the box,dots,any values you want etc.), and init of FaceDetector which helps us detect the face features such as smiling blinking and if needed around I think 24 common points of the face to detect custom features.
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: java; title: ; notranslate" title="">
    public void onCreate(Bundle icicle) {
        super.onCreate(icicle);
        setContentView(R.layout.activity_main);

        AdView mAdView = (AdView) findViewById(R.id.adView);
        AdRequest adRequest = new AdRequest.Builder().build();
        mAdView.loadAd(adRequest);

        mPreview = (CameraSourcePreview) findViewById(R.id.preview);
        mGraphicOverlay = (GraphicOverlay) findViewById(R.id.faceOverlay);
        mImageView = (ImageView) findViewById(R.id.imageView);
        mJokeView = (TextView) findViewById(R.id.jokeView);
        mImageView.setVisibility(View.INVISIBLE);

        Context context = getApplicationContext();
        FaceDetector detector = new FaceDetector.Builder(context)
                .setClassificationType(FaceDetector.ALL_CLASSIFICATIONS)
                .setProminentFaceOnly(true)
                .build();
        detector.setProcessor(
                new MultiProcessor.Builder&lt;&gt;(new GraphicFaceTrackerFactory()).build());


        if (!detector.isOperational()) {
            // Note: The first time that an app using face API is installed on a device, GMS will
            // download a native library to the device in order to do detection.  Usually this
            // completes before the app is run for the first time.  But if that download has not yet
            // completed, then the above call will not detect any faces.
            //
            // isOperational() can be used to check if the required native library is currently
            // available.  The detector will automatically become operational once the library
            // download completes on device.
            Log.w(TAG, "Face detector dependencies are not yet available.");
        }
</pre>
        
        <p>
          With continue with init of Camera, with settings of preview resolutoin, which camera to use, FPS speed etc, we also init TTS(Google&#8217;s text to speech system which we use in combination with our Google Vision API)
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: java; title: ; notranslate" title="">
        mCameraSource = new CameraSource.Builder(context, detector)
                .setRequestedPreviewSize(640, 480)
                .setFacing(CameraSource.CAMERA_FACING_FRONT)
                .setRequestedFps(30.0f)
                .build();
        mTts = new TextToSpeech(MainActivity.this, new TextToSpeech.OnInitListener(){
            @Override
            public void onInit(int status) {
                // TODO Auto-generated method stub
                if(status == TextToSpeech.SUCCESS){
                    int result=mTts.setLanguage(Locale.US);
                    if(result==TextToSpeech.LANG_MISSING_DATA ||
                            result==TextToSpeech.LANG_NOT_SUPPORTED){
                        Log.e("error", "This Language is not supported");
                    }
                    else{
                        if (android.os.Build.VERSION.SDK_INT&gt;=21){
                            mTts.speak("Welcome to: Do you smile?", TextToSpeech.QUEUE_ADD, null, "ss"); //based on text, it gets transformed to voice of Google woman
                            mTts.speak("Scan your current mood! Do you smile or not is the question?\nClick and find out!", TextToSpeech.QUEUE_ADD, null, "ss");
                        }
                        else{
                            mTts.speak("Welcome to: Do you smile?", TextToSpeech.QUEUE_ADD, null);
                            mTts.speak("Scan your current mood! Do you smile or not is the question?\nClick and find out!", TextToSpeech.QUEUE_ADD, null);
                        }
                    }
                }
                else
                    Log.e("error", "Initilization Failed!");
            }
        });

        Button button =  (Button) findViewById(R.id.takepicturebutton); //take mood picture
        button.setOnClickListener(new View.OnClickListener() {
            public void onClick(View v) {
                mImageView.setVisibility(View.INVISIBLE);
                mPreview.takeImage(); // take image function together with later main processing part. 
            }
        });

        //Main init of sample data
        initJokeStrings(); 
        initInspiriStrings();

    }
</pre>
        
        <p>
          Several smaller relevant methods, mostly for pausing,restarting, and clearing the memory of device with some minor management:
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: java; title: ; notranslate" title="">
    /**
     * Restarts the camera.
     */
    @Override
    protected void onResume() {
        super.onResume();
        startCameraSource();
    }

    /**
     * Stops the camera.
     */
    @Override
    protected void onPause() {
        super.onPause();
        mPreview.stop();
    }

    /**
     * Releases the resources associated with the camera source, the associated detector, and the
     * rest of the processing pipeline.
     */
    @Override
    protected void onDestroy() {
        super.onDestroy();
        mCameraSource.release();
    }

    //==============================================================================================
    // Camera Source Preview
    //==============================================================================================

    /**
     * Starts or restarts the camera source, if it exists.  If the camera source doesn't exist yet
     * (e.g., because onResume was called before the camera source was created), this will be called
     * again when the camera source is created.
     */
    private void startCameraSource() {
        try {
            mPreview.start(mCameraSource, mGraphicOverlay);
        } catch (IOException e) {
            Log.e(TAG, "Unable to start camera source.", e);
            mCameraSource.release();
            mCameraSource = null;
        }
    }
</pre>
        
        <p>
          Graphic face tracker initialization part:
        </p>
        
        <p>
          In this part we have some interesting methods for further investigation.<br /> One of them is setImageViewPicture. I know mostly it&#8217;s simple but the interesting part is the
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: java; title: ; notranslate" title="">
mImageView.setImageBitmap(BitmapFactory.decodeByteArray(data, 0, data.length));
</pre>
        
        <p>
          line. Since it uses the provided byte data and decodes it to an imageView. After that it goes to either get inspirational quote or get random joke, depending on the float value of your smile determined in a later covered function and class.
        </p>
        
        <p>
          The second part of this code initializes its own instance for every face in the picture, but for our demo we are only utilizing the first and most prominent face.
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: java; title: ; notranslate" title="">
    //==============================================================================================
    // Graphic Face Tracker
    //==============================================================================================

    /**
     * Factory for creating a face tracker to be associated with a new face.  The multiprocessor
     * uses this factory to create face trackers as needed -- one for each individual.
     */
    private class GraphicFaceTrackerFactory implements MultiProcessor.Factory&lt;Face&gt; {
        @Override
        public Tracker&lt;Face&gt; create(Face face) {
            return new GraphicFaceTracker(mGraphicOverlay);
        }
    }

    public void setImageViewPicture(final byte[] data){
        mImageView.setVisibility(View.VISIBLE);
        mImageView.setImageBitmap(BitmapFactory.decodeByteArray(data, 0, data.length));
        if(smileValue &gt;= 0.50f){
            getInspirationalQoute(); // You are smiling
        }
        else{
            getRandomJoke(); //You do not smile
        }
    }

    /**
     * Face tracker for each detected individual. This maintains a face graphic within the app's
     * associated face overlay.
     */
    private class GraphicFaceTracker extends Tracker&lt;Face&gt; {
        private GraphicOverlay mOverlay;
        private FaceGraphic mFaceGraphic;

        GraphicFaceTracker(GraphicOverlay overlay) {
            mOverlay = overlay;
            mFaceGraphic = new FaceGraphic(overlay);
        }

        /**
         * Start tracking the detected face instance within the face overlay.
         */
        @Override
        public void onNewItem(int faceId, Face item) {
            mFaceGraphic.setId(faceId);
        }

        /**
         * Update the position/characteristics of the face within the overlay.
         */
        @Override
        public void onUpdate(FaceDetector.Detections&lt;Face&gt; detectionResults, Face face) {
            mOverlay.add(mFaceGraphic);
            mFaceGraphic.updateFace(face);
            smileValue = mFaceGraphic.getSmileProbability();
        }

        /**
         * Hide the graphic when the corresponding face was not detected.  This can happen for
         * intermediate frames temporarily (e.g., if the face was momentarily blocked from
         * view).
         */
        @Override
        public void onMissing(FaceDetector.Detections&lt;Face&gt; detectionResults) {
            mOverlay.remove(mFaceGraphic);
        }

        /**
         * Called when the face is assumed to be gone for good. Remove the graphic annotation from
         * the overlay.
         */
        @Override
        public void onDone() {
            mOverlay.remove(mFaceGraphic);
        }
    }
</pre>
        
        <p>
          The fun part with jokes and qoutes:
        </p>
        
        <p>
          Based as seen before on Smile probability from Google Vision API we can now go to for example a getRandomJoke function. Here we first check if the Android version is bigger then 21 or smaller, since based on the version i noticed then can sometimes be problemds due to one version of TTS speak function getting deprecated in newer versions, thats why I am separating both of them. It also accesses the string arrays and picks up random string value of quote or joke, to try to make you happy if you are sad, or just make you wiser if you smile enough already.
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: java; title: ; notranslate" title="">
   public void getRandomJoke(){
        if (android.os.Build.VERSION.SDK_INT&gt;=21){
            String joke = jokes[new Random().nextInt(jokes.length)];
            mTts.speak(joke, TextToSpeech.QUEUE_FLUSH, null, "ss");
            mJokeView.setText("Joke, cause you don't smile:" + "\n" + joke);
        }
        else{
            mTts.speak(jokes[new Random().nextInt(jokes.length)], TextToSpeech.QUEUE_FLUSH, null);
        }
    }

    public void getInspirationalQoute() {
        if (android.os.Build.VERSION.SDK_INT&gt;=21){
            String quote = quotes[new Random().nextInt(quotes.length)];
            mTts.speak(quote, TextToSpeech.QUEUE_FLUSH, null, "ss");
            mJokeView.setText("Quote, cause you smile:" + "\n" + quote);
        }
        else{
            mTts.speak(quotes[new Random().nextInt(quotes.length)], TextToSpeech.QUEUE_FLUSH, null);
        }
    }
</pre>
        
        <p>
          Just for the sake of complete code the not so fine done array of jokes and qoutes.
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: java; title: ; notranslate" title="">
    public void initJokeStrings(){
        jokes = new String[] {
                "The clear history button in your browser has saved more lives than Superman",
                "I bet earth makes fun of the other planets for having no life",
                "Oh no! Playstation and Xbox online services are down! Someone call an ambulance! Wii U Wii U Wii U.",
                "The sight of a woman's cleavage reduces a man's ability to think clearly by 50%... per boob!",
                "Jimmy has 42 candy bars. Jimmy eats 24. What does jimmy have now? Diabetes.. Jimmy has diabetes.",
                "What type of Bee's make milk instead of honey? Boobies",
                "I gave my number to a really hot girl at the bar and told her to text me when she got home. She must be homeless",
                "Just changed my Facebook name to ‘No one' so when I see stupid posts I can click like and it will say ‘No one likes this'.",
                "What's the difference between snowmen and snowladies? Snowballs",
                "How do you make holy water? You boil the hell out of it.",
                "If con is the opposite of pro, it must mean Congress is the opposite of progress?",
                "I wondered why the frisbee was getting bigger, and then it hit me.",
                "I used to like my neighbors, until they put a password on their Wi-Fi.",
                "Never argue with a fool, they will lower you to their level, and then beat you with experience.",
                "Why do farts smell? So deaf people can enjoy them too.",
                "Light travels faster than sound. This is why some people appear bright until they speak.",
                "What did the ocean say to the beach? Nothing, it just waved.",
                "I say no to alcohol, it just doesn't listen.",
                "Why did the skeleton go to the party alone? -- He had no body to go with him!",
                "Right now I'm having amnesia and deja vu at the same time! I think I've forgotten this before?",
                "Why is Peter Pan always flying? Because he Neverlands.",
                "I think i want a job cleaning mirrors, It's just something i could really see myself doing",
                "My girlfriend keeps going on bout the time i jokingly put superglue on her mobile phone, honestly , she just can't let it go.",
                "How do you make a tissue dance? You put a little boogie in it.",
                "For Christmas, I want Santa's list of naughty girls.",
                "Who says nothing is impossible. I've been doing nothing for years."
        };
    }

    public void initInspiriStrings(){
        quotes = new String[] {
                "Things may come to those who wait, but only the things left by those who hustle. By Abraham Lincoln",
                "The great secret of education is to direct vanity to proper objects. By Adam Smith",
                "It’s not that travel just broadens your mind, rather it enables you to see how narrow your oppressor’s minds are. By Alain de Botton",
                "A person who never made a mistake never tried anything new. By Alan Watts",
                "Better to have a short life that is full of what you like doing than a long life spent in a miserable way. By Alan Watts",
                "Life is a musical thing and you are supposed to dance and sign while it's being played. By Alan Watts",
                "Omnipotence is not knowing how everything is done; it's just doing it. By Alan Watts",
                "It is not humiliating to be unhappy. Physical suffering is sometimes humiliating, but the suffering of being cannot be, it is life. By Albert Camus",
                "Learn from yesterday, live for today, hope for tomorrow. The important thing is not to stop questioning. By Albert Einstein",
                "The secret to creativity is knowing how to hide your sources. By Albert Einstein",
                "The true sign of intelligence is not knowledge but imagination. By Albert Einstein",
                "The world as we have created it is a process of our thinking. It cannot be changed without changing our thinking. By Albert Einstein",
                "When facts don't fit the theory, change the facts. By Albert Einstein",
                "Creativity never comes under emotional stress or tension. The real creativity comes when the mind finally relaxes and is quiet and then can focus. By Amar Bose",
                "If you think something is impossible, don't disturb the person doing it. By Amar Bose",
                "If you want to build a ship, don't drum up people to collect wood and don't assign them tasks and work, but rather teach them to long for the endless immensity of the sea. By Antoine de Saint-Exupery",
                "To love is not to look at one another: it is to look, together, in the same direction. By Antoine de Saint-Exupery",
                "When you give yourself, you receive more than you give. By Antoine de Saint-Exupery",
                "Do not fear to be eccentric in opinion, for every opinion now accepted was once eccentric. By Bertrand Russell",
                "Visionaries not only believe that the impossible can be done, but that it must be done. By Bran Ferren",
                "People who have a strong sense of love and belonging believe they're worthy of it. By Brene Brown",
                "Every human being has some flavor of ‘not enough.’ You can either be stopped by it, or simply notice it, like the weather. By Brigid Schulte",
                "Anyone can complain about the world, but only a good few can fix it. By Cennydd Bowles",
                "So many people rush through life, let's take our time living it. By Christian Vuerings",
                "The more that you read, the more things you will know. The more that you learn, the more places you’ll go. By Doctor Seuss",
                "Dichotomy between sense of wonder and what is wrong. By Elon Musk",
                "If something is important enough, you should try. Even if the probable outcome is failure. By Elon Musk",
                "There's skepticism about anything new. That's normal. By Elon Musk",
                "There is only one way to happiness and that is to cease worrying about things which are beyond the power of our will. By Epictetus",
                "There are 2 ways to make a man richer, give him more money or curb his desires. By Jean-Jacques Rousseau",
                "Being deeply loved by someone gives you strength, while loving someone deeply gives you courage. By Lao Tse",
                "A leader is best when people barely know he exists, when his work is done, his aim fulfilled, they will say: we did it ourselves. By Lao Tse",
                "Silence is a source of great strength. By Lao Tse",
                "To attain knowledge, add things every day. To attain wisdom, remove things every day. By Lao Tse",
                "The best way to have a good idea is to have lots of ideas. By Linus Pauling",
                "At home I am a nice guy: but I don't want the world to know. Humble people, I've found, don't get very far. By Muhammad Ali",
                "He who is not courageous enough to take risks will accomplish nothing in life. By Muhammad Ali",
                "I am the greatest, I said that even before I knew I was. By Muhammad Ali",
                "It isn't the mountains ahead to climb that wear you out; it's the pebble in your shoe. By Muhammad Ali",
                "The man who has no imagination has no wings. By Muhammad Ali",
                "If there is no struggle, there is no progress. By Frederick Douglass",
                "Success is a state of being. Because as soon as you say you're successful, you probably start to fail. By Howard H. Stevenson",
                "The reasonable man adapts himself to the world; the unreasonable one persists in trying to adapt the world to himself. Therefore, all progress depends on the unreasonable man. By George Bernard Shaw",
                "Life would be much easier to understand if mother nature gave us the source code. By Graeme MacWilliam",
                "Coming together is a beginning; keeping together is progress; staying together is success. By Henry Ford",
                "An ounce of experience is better than a ton of theory simply. By John Dewey",
                "A journey of a thousand miles begins with a single step. By Laozi",
                "A man is but the product of his thoughts what he thinks, he becomes. By Mahatma Gandhi",
                "An ounce of practice is worth more than tons of preaching. By Mahatma Gandhi",
                "Live as if you were to die tomorrow. Learn as if you were to live forever. By Mahatma Gandhi",
                "You must be the change you wish to see in the world. By Mahatma Gandhi",
                "You must be the change you wish to see in the world. By Mahatma Gandhi",
                "I have never let my schooling interfere with my education. By Mark Twain",
                "Never let the future disturb you. You will meet it, if you have to, with the same weapons of reason which today arm you against the present. By ",
                "Never believe that a few caring people can't change the world. For, indeed, that's all who ever have. By ",
                "Keep away from those who try to belittle your ambitions. Small people always do that, but the really great make you believe that you too can become great. By ",
                "Life is short, break the rules. By ",
                "A gentleman is one who never hurts anyone's feelings unintentionally. By Oscar Wilde",
                "A man who does not think for himself does not think at all. By Oscar Wilde",
                "Always forgive your enemies - nothing annoys them so much. By Oscar Wilde",
                "America is the only country that went from barbarism to decadence without civilization in between. By Oscar Wilde",
                "Between men and women there is no friendship possible. There is passion, enmity, worship, love, but no friendship. By Oscar Wilde",
                "Education is an admirable thing, but it is well to remember from time to time that nothing that is worth knowing can be taught. By Oscar Wilde",
                "Experience is simply the name we give our mistakes. By Oscar Wilde",
                "If you want to tell people the truth, make them laugh, otherwise they’ll kill you. By Oscar Wilde",
                "There are only two tragedies in life: one is not getting what one wants, and the other is getting it. By Oscar Wilde",
                "Work is the curse of the drinking classes. By Oscar Wilde",
                "If you’re far enough ahead that people can’t figure out if you’re joking, you know you’ve innovated. By Paul Buchheit",
                "The first thing I do on day one is build something useful, then just keep improving it. By Paul Buchheit",
                "Go where you’re celebrated, not where you’re tolerated. By Paul F. Davis",
                "Maintain your spirit of curiosity, keep questioning things, and you’ll find new ways to innovate. By Richard Brandson",
                "If I look confused it is because I am thinking. By Samuel Goldwyn",
                "The harder I work, the luckier I get. By Samuel Goldwyn",
                "When someone does a good job, applaud; it makes two people happy. By Samuel Goldwyn",
                "Defenseless is the best choice for those seeking to grow. By Seth Godin",
                "Ship often. Ship lousy stuff, but ship. Ship constantly. By Seth Godin",
                "If you do something and it turns out pretty good, then you should go do something else wonderful, not dwell on it for too long. Just figure out what’s next. By Steve Jobs",
                "Do not go where the path may lead, go instead where there is no path and leave a trail. By Ralph Waldo Emerson",
                "For every minute you remain angry, you give up sixty seconds of peace of mind. By Ralph Waldo Emerson",
                "Nothing great was ever achieved without enthusiasm. By Ralph Waldo Emerson",
                "If you’re not a embarrassed by the first version of your product, you launched to late. By Reid Hoffman",
                "You earn trust by providing innovative, quality products and keeping your word. By Richard Brandson",
                "Nothing comes to a sleeper but a dream. By Richard Williams",
                "While we teach, we learn. By Seneca The Younger",
                "Being the richest man in the cemetery doesn’t matter to me … Going to bed at night saying we’ve done something wonderful… that’s what matters to me. By Steve Jobs",
                "One must learn by doing the thing; for though you think you know it, you have no certainty until you try. By Sophocles",
                "The enemy of sustainable productivity is not stress. Rather, it’s the absence of intermittent rest and renewal. By Tony Schwartz",
                "I keep going anyway. I pause and take the doubts in. I cry. I curse. I think it's unfair and that I can't continue. But then I do. I get up, brush my shoulders off, and carry on. By Tiffany Han",
                "A man is not idle because he is absorbed in thought. There is a visible labor and there is an invisible labor. By Victor Hugo",
                "He who opens a school door, closes a prison. By Victor Hugo",
                "Initiative is doing the right thing without being told. By Victor Hugo",
                "There is nothing more powerful than an idea whose time has come. By Victor Hugo",
                "When a woman is talking to you, listen to what she says with her eyes. By Victor Hugo",
                "Being male is a matter of birth. Being a man is a matter of age. But being a Gentleman is a matter of choice. By Vin Diesel",
                "Education shouldn't fill a bucket but light a fire. By William Butler Yeats",
                "There are no strangers here; Only friends you haven't yet met. By William Butler Yeats",
        };
    }
</pre>
        
        <div class="fusion-button-wrapper fusion-aligncenter">
          <a class="fusion-button button-flat fusion-button-round button-large button-blue button-1" target="_self" href="https://codeandunicorns.com/android-google-vision-api-project-example-part-2"><span class="fusion-button-text">Go to part 2</span></a>
        </div>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
  </div>
</div>