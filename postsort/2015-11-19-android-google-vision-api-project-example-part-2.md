---
id: 1501
title: Android Google Vision API project example part 2
date: 2015-11-19T15:47:51+00:00
author: Matjaz Trcek
layout: post
guid: https://codeandunicorns.com/?p=1501
permalink: /android-google-vision-api-project-example-part-2/
slide_template:
  - default
fusion_builder_status:
  - inactive
avada_post_views_count:
  - "7952"
dsq_thread_id:
  - "4333245457"
fusion_builder_content_backup:
  - |
    In this part of the code we are going in depth of overlays of previews and Google Vision API. The next part of the code will be properly commented so the read out should be easier
    
    <h2>JAVA part</h2>
    
    [code lang="java"]
    /**
    * Created by mitola on 22/08/15.
    */
    public class FaceView extends View {
    private Bitmap mBitmap; // Initi of Bitmap
    private SparseArray&amp;amp;lt;Face&amp;amp;gt; mFaces; // And Faces
    
    public FaceView(Context context, AttributeSet attrs) {
    super(context, attrs);
    }
    
    void setContent(Bitmap bitmap, SparseArray&amp;amp;lt;Face&amp;amp;gt; faces) {
    mBitmap = bitmap;
    mFaces = faces;
    invalidate();
    }
    
    @Override
    protected void onDraw(Canvas canvas) {
    super.onDraw(canvas);
    if ((mBitmap != null) &amp;amp;amp;&amp;amp;amp; (mFaces != null)) {
    double scale = drawBitmap(canvas);
    drawFaceAnnotations(canvas, scale);
    }
    }
    
    private double drawBitmap(Canvas canvas) {
    //to draw the bitmap scaled to the device size
    double viewWidth = canvas.getWidth();
    double viewHeight = canvas.getHeight();
    double imageWidth = mBitmap.getWidth();
    double imageHeight = mBitmap.getHeight();
    double scale = Math.min(viewWidth / imageWidth, viewHeight / imageHeight);
    
    Rect destBounds = new Rect(0, 0, (int) (imageWidth * scale), (int) (imageHeight * scale));
    canvas.drawBitmap(mBitmap, null, destBounds, null);
    return scale;
    }
    
    private void drawFaceAnnotations(Canvas canvas, double scale) {
    //create paint to draw on the image
    Paint paint = new Paint();
    paint.setColor(Color.GREEN);
    paint.setStyle(Paint.Style.STROKE); //no fill
    paint.setStrokeWidth(5);
    
    //make a rectangle to follow with the face
    for (int i = 0; i &amp;amp;lt; mFaces.size(); ++i) {
    Face face = mFaces.valueAt(i);
    float x1 = face.getPosition().x; //x coordinate of top left position of the face within the image
    float y1 = face.getPosition().y; //x coordinate of top left position of the face within the image
    float x2 = x1 + face.getWidth(); //width of the face region in pixels
    float y2 = y1 + face.getHeight(); //heightof the face region in pixels
    canvas.drawRoundRect(new RectF(x1 * (float) scale, y1 * (float) scale, x2 * (float) scale, y2 * (float) scale), 2, 2, paint);
    }
    }
    }
    [/code]
    
    In this part you can explore the graphical overlay, which focuses mostly on making a box around the face so you know you are getting it tracked, and also used for debugging with anything you need on the screen preview. In previous testing version I was using it for example for writing smile probability value.
    
    [code lang="java"]
    /**
    * Graphic instance for rendering face position, orientation, and landmarks within an associated
    * graphic overlay view.
    */
    class FaceGraphic extends GraphicOverlay.Graphic {
    private static final float FACE_POSITION_RADIUS = 10.0f;
    private static final float ID_TEXT_SIZE = 40.0f;
    private static final float ID_Y_OFFSET = 50.0f;
    private static final float ID_X_OFFSET = -50.0f;
    private static final float BOX_STROKE_WIDTH = 5.0f;
    public float smileValue = 1.0f;
    
    private static final int COLOR_CHOICES[] = {
    Color.BLUE,
    Color.CYAN,
    Color.GREEN,
    Color.MAGENTA,
    Color.RED,
    Color.WHITE,
    Color.YELLOW
    };
    private static int mCurrentColorIndex = 0;
    
    private Paint mFacePositionPaint;
    private Paint mIdPaint;
    private Paint mBoxPaint;
    
    private volatile Face mFace;
    private int mFaceId;
    
    FaceGraphic(GraphicOverlay overlay) {
    super(overlay);
    
    mCurrentColorIndex = (mCurrentColorIndex + 1) % COLOR_CHOICES.length;
    final int selectedColor = COLOR_CHOICES[mCurrentColorIndex];
    
    mFacePositionPaint = new Paint();
    mFacePositionPaint.setColor(selectedColor);
    
    mIdPaint = new Paint();
    mIdPaint.setColor(selectedColor);
    mIdPaint.setTextSize(ID_TEXT_SIZE);
    
    mBoxPaint = new Paint();
    mBoxPaint.setColor(selectedColor);
    mBoxPaint.setStyle(Paint.Style.STROKE);
    mBoxPaint.setStrokeWidth(BOX_STROKE_WIDTH);
    }
    
    void setId(int id) {
    mFaceId = id;
    }
    
    /**
    * Updates the face instance from the detection of the most recent frame.  Invalidates the
    * relevant portions of the overlay to trigger a redraw.
    */
    void updateFace(Face face) {
    mFace = face;
    postInvalidate();
    }
    
    /**
    * Draws the face annotations for position on the supplied canvas.
    */
    @Override
    public void draw(Canvas canvas) {
    Face face = mFace;
    if (face == null) {
    return;
    }
    
    // Draws a circle at the position of the detected face, with the face's track id below.
    float x = translateX(face.getPosition().x + face.getWidth() / 2);
    float y = translateY(face.getPosition().y + face.getHeight() / 2);
    canvas.drawCircle(x, y, FACE_POSITION_RADIUS, mFacePositionPaint);
    //USED FOR DEBUGGING , TODO: cleanup
    //canvas.drawText(&quot;id: &quot; + mFaceId, x + ID_X_OFFSET, y + ID_Y_OFFSET, mIdPaint); //this can be used for extra debuging such as marking each of the faces with its own ID, rectangle
    smileValue=face.getIsSmilingProbability();
    //canvas.drawText(Float.toString(smileValue), x + ID_X_OFFSET, y + ID_Y_OFFSET*2, mIdPaint);
    
    /*if(smileValue &amp;amp;gt;= 0.5f){
    canvas.drawText(&quot;YOU ARE SMILING&quot;, x + ID_X_OFFSET, y + ID_Y_OFFSET*3, mIdPaint);
    }*/
    
    // Draws a bounding box around the face.
    float xOffset = scaleX(face.getWidth() / 2.0f);
    float yOffset = scaleY(face.getHeight() / 2.0f);
    float left = x - xOffset;
    float top = y - yOffset;
    float right = x + xOffset;
    float bottom = y + yOffset;
    canvas.drawRect(left, top, right, bottom, mBoxPaint);
    }
    
    public float getSmileProbability(){
    return smileValue;
    }
    }
    [/code]
    
    In the CameraSourcePreview the code is gotten from part of the samples of the Google Vision API. I think the code should be quite understandable, but if not feel free to ask questions so I can answer them and add them if needed to the blog post as well.
    
    [code lang="java"]
    public class CameraSourcePreview extends ViewGroup {
    private static final String TAG = &quot;CameraSourcePreview&quot;;
    
    private Context mContext;
    private SurfaceView mSurfaceView;
    private boolean mStartRequested;
    private boolean mSurfaceAvailable;
    private CameraSource mCameraSource;
    
    private GraphicOverlay mOverlay;
    
    public CameraSourcePreview(Context context, AttributeSet attrs) {
    super(context, attrs);
    mContext = context;
    mStartRequested = false;
    mSurfaceAvailable = false;
    
    mSurfaceView = new SurfaceView(context);
    mSurfaceView.getHolder().addCallback(new SurfaceCallback());
    addView(mSurfaceView);
    }
    
    public void start(CameraSource cameraSource) throws IOException {
    if (cameraSource == null) {
    stop();
    }
    
    mCameraSource = cameraSource;
    
    if (mCameraSource != null) {
    mStartRequested = true;
    startIfReady();
    }
    }
    
    public void start(CameraSource cameraSource, GraphicOverlay overlay) throws IOException {
    mOverlay = overlay;
    start(cameraSource);
    }
    
    public void stop() {
    if (mCameraSource != null) {
    mCameraSource.stop();
    }
    }
    
    public void release() {
    if (mCameraSource != null) {
    mCameraSource.release();
    mCameraSource = null;
    }
    }
    
    private void startIfReady() throws IOException {
    if (mStartRequested &amp;amp;amp;&amp;amp;amp; mSurfaceAvailable) {
    mCameraSource.start(mSurfaceView.getHolder());
    if (mOverlay != null) {
    Size size = mCameraSource.getPreviewSize();
    int min = Math.min(size.getWidth(), size.getHeight());
    int max = Math.max(size.getWidth(), size.getHeight());
    if (isPortraitMode()) {
    // Swap width and height sizes when in portrait, since it will be rotated by
    // 90 degrees
    mOverlay.setCameraInfo(min, max, mCameraSource.getCameraFacing());
    } else {
    mOverlay.setCameraInfo(max, min, mCameraSource.getCameraFacing());
    }
    mOverlay.clear();
    }
    mStartRequested = false;
    }
    }
    
    private class SurfaceCallback implements SurfaceHolder.Callback {
    @Override
    public void surfaceCreated(SurfaceHolder surface) {
    mSurfaceAvailable = true;
    try {
    startIfReady();
    } catch (IOException e) {
    Log.e(TAG, &quot;Could not start camera source.&quot;, e);
    }
    }
    
    @Override
    public void surfaceDestroyed(SurfaceHolder surface) {
    mSurfaceAvailable = false;
    }
    
    @Override
    public void surfaceChanged(SurfaceHolder holder, int format, int width, int height) {
    }
    }
    
    @Override
    protected void onLayout(boolean changed, int left, int top, int right, int bottom) {
    int width = 320;
    int height = 240;
    if (mCameraSource != null) {
    Size size = mCameraSource.getPreviewSize();
    if (size != null) {
    width = size.getWidth();
    height = size.getHeight();
    }
    }
    
    // Swap width and height sizes when in portrait, since it will be rotated 90 degrees
    if (isPortraitMode()) {
    int tmp = width;
    width = height;
    height = tmp;
    }
    
    final int layoutWidth = right - left;
    final int layoutHeight = bottom - top;
    
    // Computes height and width for potentially doing fit width.
    int childWidth = layoutWidth;
    int childHeight = (int)(((float) layoutWidth / (float) width) * height);
    
    // If height is too tall using fit width, does fit height instead.
    if (childHeight &amp;amp;gt; layoutHeight) {
    childHeight = layoutHeight;
    childWidth = (int)(((float) layoutHeight / (float) height) * width);
    }
    
    for (int i = 0; i &amp;amp;lt; getChildCount(); ++i) {
    getChildAt(i).layout(0, 0, childWidth, childHeight);
    }
    
    try {
    startIfReady();
    } catch (IOException e) {
    Log.e(TAG, &quot;Could not start camera source.&quot;, e);
    }
    }
    
    private boolean isPortraitMode() {
    int orientation = mContext.getResources().getConfiguration().orientation;
    if (orientation == Configuration.ORIENTATION_LANDSCAPE) {
    return false;
    }
    if (orientation == Configuration.ORIENTATION_PORTRAIT) {
    return true;
    }
    
    Log.d(TAG, &quot;isPortraitMode returning false by default&quot;);
    return false;
    }
    
    public void takeImage(){
    mCameraSource.takePicture(null, callbackPicture);
    }
    private ImageView imageView;
    
    CameraSource.PictureCallback callbackPicture = new CameraSource.PictureCallback(){
    public void onPictureTaken(final byte[] data)
    {
    if(mContext instanceof MainActivity) {
    MainActivity main = (MainActivity)mContext;
    main.setImageViewPicture(data);
    }
    }
    };
    
    }
    [/code]
    
    
    Quite similar story goes for GraphicOverlay as well.
    
    [code lang="java"]
    /**
    * A view which renders a series of custom graphics to be overlayed on top of an associated preview
    * (i.e., the camera preview).  The creator can add graphics objects, update the objects, and remove
    * them, triggering the appropriate drawing and invalidation within the view.
    
    *
    * Supports scaling and mirroring of the graphics relative the camera's preview properties.  The
    * idea is that detection items are expressed in terms of a preview size, but need to be scaled up
    * to the full view size, and also mirrored in the case of the front-facing camera.
    
    *
    * Associated {@link Graphic} items should use the following methods to convert to view coordinates
    * for the graphics that are drawn:
    *
    &amp;amp;lt;ol&amp;amp;gt;
    *
    &amp;amp;lt;li&amp;amp;gt;{@link Graphic#scaleX(float)} and {@link Graphic#scaleY(float)} adjust the size of the
    * supplied value from the preview scale to the view scale.&amp;amp;lt;/li&amp;amp;gt;
    
    *
    &amp;amp;lt;li&amp;amp;gt;{@link Graphic#translateX(float)} and {@link Graphic#translateY(float)} adjust the coordinate
    * from the preview's coordinate system to the view coordinate system.&amp;amp;lt;/li&amp;amp;gt;
    
    * &amp;amp;lt;/ol&amp;amp;gt;
    
    */
    public class GraphicOverlay extends View {
    private final Object mLock = new Object();
    private int mPreviewWidth;
    private float mWidthScaleFactor = 1.0f;
    private int mPreviewHeight;
    private float mHeightScaleFactor = 1.0f;
    private int mFacing = CameraSource.CAMERA_FACING_BACK;
    private Set&amp;amp;lt;Graphic&amp;amp;gt; mGraphics = new HashSet&amp;amp;lt;&amp;amp;gt;();
    
    /**
    * Base class for a custom graphics object to be rendered within the graphic overlay.  Subclass
    * this and implement the {@link Graphic#draw(Canvas)} method to define the
    * graphics element.  Add instances to the overlay using {@link GraphicOverlay#add(Graphic)}.
    */
    public static abstract class Graphic {
    private GraphicOverlay mOverlay;
    
    public Graphic(GraphicOverlay overlay) {
    mOverlay = overlay;
    }
    
    /**
    * Draw the graphic on the supplied canvas.  Drawing should use the following methods to
    * convert to view coordinates for the graphics that are drawn:
    *
    &amp;amp;lt;ol&amp;amp;gt;
    *
    &amp;amp;lt;li&amp;amp;gt;{@link Graphic#scaleX(float)} and {@link Graphic#scaleY(float)} adjust the size of
    * the supplied value from the preview scale to the view scale.&amp;amp;lt;/li&amp;amp;gt;
    
    *
    &amp;amp;lt;li&amp;amp;gt;{@link Graphic#translateX(float)} and {@link Graphic#translateY(float)} adjust the
    * coordinate from the preview's coordinate system to the view coordinate system.&amp;amp;lt;/li&amp;amp;gt;
    
    * &amp;amp;lt;/ol&amp;amp;gt;
    
    *
    * @param canvas drawing canvas
    */
    public abstract void draw(Canvas canvas);
    
    /**
    * Adjusts a horizontal value of the supplied value from the preview scale to the view
    * scale.
    */
    public float scaleX(float horizontal) {
    return horizontal * mOverlay.mWidthScaleFactor;
    }
    
    /**
    * Adjusts a vertical value of the supplied value from the preview scale to the view scale.
    */
    public float scaleY(float vertical) {
    return vertical * mOverlay.mHeightScaleFactor;
    }
    
    /**
    * Adjusts the x coordinate from the preview's coordinate system to the view coordinate
    * system.
    */
    public float translateX(float x) {
    if (mOverlay.mFacing == CameraSource.CAMERA_FACING_FRONT) {
    return mOverlay.getWidth() - scaleX(x);
    } else {
    return scaleX(x);
    }
    }
    
    /**
    * Adjusts the y coordinate from the preview's coordinate system to the view coordinate
    * system.
    */
    public float translateY(float y) {
    return scaleY(y);
    }
    
    public void postInvalidate() {
    mOverlay.postInvalidate();
    }
    }
    
    public GraphicOverlay(Context context, AttributeSet attrs) {
    super(context, attrs);
    }
    
    /**
    * Removes all graphics from the overlay.
    */
    public void clear() {
    synchronized (mLock) {
    mGraphics.clear();
    }
    postInvalidate();
    }
    
    /**
    * Adds a graphic to the overlay.
    */
    public void add(Graphic graphic) {
    synchronized (mLock) {
    mGraphics.add(graphic);
    }
    postInvalidate();
    }
    
    /**
    * Removes a graphic from the overlay.
    */
    public void remove(Graphic graphic) {
    synchronized (mLock) {
    mGraphics.remove(graphic);
    }
    postInvalidate();
    }
    
    /**
    * Sets the camera attributes for size and facing direction, which informs how to transform
    * image coordinates later.
    */
    public void setCameraInfo(int previewWidth, int previewHeight, int facing) {
    synchronized (mLock) {
    mPreviewWidth = previewWidth;
    mPreviewHeight = previewHeight;
    mFacing = facing;
    }
    postInvalidate();
    }
    
    /**
    * Draws the overlay with its associated graphic objects.
    */
    @Override
    protected void onDraw(Canvas canvas) {
    super.onDraw(canvas);
    
    synchronized (mLock) {
    if ((mPreviewWidth != 0) &amp;amp;amp;&amp;amp;amp; (mPreviewHeight != 0)) {
    mWidthScaleFactor = (float) canvas.getWidth() / (float) mPreviewWidth;
    mHeightScaleFactor = (float) canvas.getHeight() / (float) mPreviewHeight;
    }
    
    for (Graphic graphic : mGraphics) {
    graphic.draw(canvas);
    }
    }
    }
    }
    [/code]
    
    </h1>XML files</h1>
    And the only thing left now is the XML files such as a description of design and strings.xml file. There is also the Manifest, but I think the most important part is the application part which I am also adding at the end. Together with the Github url where you can access all the source code for this Google Vision API example.
    
    <h2>Activity_main</h2>
    This file is called activity_main.xml
    
    [code lang="xml"]
    &lt;?xml version=&quot;1.0&quot; encoding=&quot;utf-8&quot;?&gt;
    &lt;RelativeLayout
    xmlns:android=&quot;http://schemas.android.com/apk/res/android&quot;
    android:id=&quot;@+id/topLayout&quot;
    android:orientation=&quot;vertical&quot;
    android:layout_width=&quot;match_parent&quot;
    android:layout_height=&quot;match_parent&quot;
    android:columnCount=&quot;2&quot;
    android:rowCount=&quot;2&quot;
    xmlns:ads=&quot;http://schemas.android.com/apk/res-auto&quot;
    android:keepScreenOn=&quot;true&quot;&gt;
    
    &lt;com.codeandunicorns.face.doyousmile.uicamera.CameraSourcePreview
    android:id=&quot;@+id/preview&quot;
    android:layout_width=&quot;208dp&quot;
    android:layout_height=&quot;277dp&quot;
    android:layout_gravity=&quot;center|left|top&quot;&gt;
    
    &lt;/com.codeandunicorns.face.doyousmile.uicamera.CameraSourcePreview&gt;
    
    &lt;ImageView
    android:layout_width=&quot;match_parent&quot;
    android:layout_height=&quot;match_parent&quot;
    android:id=&quot;@+id/imageView&quot;
    android:layout_gravity=&quot;center_horizontal|left|top&quot;
    android:layout_alignParentTop=&quot;true&quot;
    android:layout_alignParentEnd=&quot;true&quot;
    android:layout_above=&quot;@+id/jokeView&quot;
    android:layout_toEndOf=&quot;@+id/preview&quot; /&gt;
    
    &lt;com.codeandunicorns.face.doyousmile.uicamera.GraphicOverlay
    android:id=&quot;@+id/faceOverlay&quot;
    android:layout_width=&quot;match_parent&quot;
    android:layout_height=&quot;match_parent&quot;
    android:layout_alignParentTop=&quot;true&quot;
    android:layout_alignParentStart=&quot;true&quot;
    android:layout_above=&quot;@+id/jokeView&quot;
    android:layout_toStartOf=&quot;@+id/imageView&quot; /&gt;
    
    &lt;LinearLayout
    android:orientation=&quot;vertical&quot;
    android:layout_width=&quot;match_parent&quot;
    android:layout_height=&quot;110dp&quot;
    android:layout_gravity=&quot;bottom&quot;
    android:layout_alignParentBottom=&quot;true&quot;
    android:layout_alignParentStart=&quot;true&quot;
    android:id=&quot;@+id/linearLayout&quot;
    android:gravity=&quot;center_horizontal&quot;
    android:weightSum=&quot;1&quot;&gt;
    
    &lt;Button
    android:layout_width=&quot;match_parent&quot;
    android:layout_height=&quot;wrap_content&quot;
    android:text=&quot;@string/button_main&quot;
    android:id=&quot;@+id/takepicturebutton&quot;
    android:textSize=&quot;20sp&quot; /&gt;
    
    &lt;com.google.android.gms.ads.AdView
    android:id=&quot;@+id/adView&quot;
    android:layout_width=&quot;wrap_content&quot;
    android:layout_height=&quot;wrap_content&quot;
    ads:adSize=&quot;BANNER&quot;
    ads:adUnitId=&quot;@string/banner_ad_unit_id&quot;&gt;
    &lt;/com.google.android.gms.ads.AdView&gt;
    
    &lt;/LinearLayout&gt;
    
    &lt;TextView
    android:layout_width=&quot;fill_parent&quot;
    android:layout_height=&quot;fill_parent&quot;
    android:text=&quot;@string/starting_text&quot;
    android:id=&quot;@+id/jokeView&quot;
    android:layout_gravity=&quot;right|top&quot;
    android:layout_below=&quot;@+id/preview&quot;
    android:layout_above=&quot;@+id/linearLayout&quot;
    android:textSize=&quot;17dp&quot;
    android:textIsSelectable=&quot;false&quot;
    android:paddingEnd=&quot;10dp&quot;
    android:paddingStart=&quot;10dp&quot; /&gt;
    
    
    &lt;/RelativeLayout&gt;
    [/code]
    
    <h2>Strings.xml</h2>
    This file is called strings.xml:
    
    [code lang="xml"]
    &lt;resources&gt;
    &lt;string name=&quot;app_name&quot;&gt;Do you smile?&lt;/string&gt;
    
    &lt;string name=&quot;hello_world&quot;&gt;Hello world!&lt;/string&gt;
    &lt;string name=&quot;action_settings&quot;&gt;Settings&lt;/string&gt;
    &lt;string name=&quot;banner_ad_unit_id&quot;&gt;ca-app-pub-YOURID&lt;/string&gt;
    &lt;string name=&quot;starting_text&quot;&gt;Scan your current mood! Do you smile or not is the question?nClick and find out!&lt;/string&gt;
    &lt;string name=&quot;button_main&quot;&gt;Take mood picture&lt;/string&gt;
    &lt;/resources&gt;
    [/code]
    
    <h2>AndroidManifest.xml</h2>
    
    And the AndroidManifest.xml file contents with permissions etc:
    
    [code lang="xml"]
    &lt;?xml version=&quot;1.0&quot; encoding=&quot;utf-8&quot;?&gt;
    &lt;manifest xmlns:android=&quot;http://schemas.android.com/apk/res/android&quot;
    package=&quot;com.codeandunicorns.face.doyousmile&quot; &gt;
    
    &lt;uses-feature android:name=&quot;android.hardware.camera&quot; /&gt;
    
    &lt;uses-permission android:name=&quot;android.permission.CAMERA&quot; /&gt;
    
    &lt;application
    android:allowBackup=&quot;true&quot;
    android:icon=&quot;@mipmap/ic_launcher&quot;
    android:label=&quot;@string/app_name&quot;
    android:theme=&quot;@style/AppTheme&quot;&gt;
    &lt;meta-data android:name=&quot;com.google.android.gms.version&quot;
    android:value=&quot;@integer/google_play_services_version&quot; /&gt;
    &lt;activity
    android:name=&quot;.MainActivity&quot;
    android:label=&quot;@string/app_name&quot; &gt;
    &lt;intent-filter&gt;
    &lt;action android:name=&quot;android.intent.action.MAIN&quot; /&gt;
    
    &lt;category android:name=&quot;android.intent.category.LAUNCHER&quot; /&gt;
    &lt;/intent-filter&gt;
    &lt;/activity&gt;
    &lt;meta-data
    android:name=&quot;com.google.android.gms.vision.DEPENDENCIES&quot;
    android:value=&quot;face&quot; /&gt;
    &lt;activity android:name=&quot;com.google.android.gms.ads.AdActivity&quot;
    android:configChanges=&quot;keyboard|keyboardHidden|orientation|screenLayout|uiMode|screenSize|smallestScreenSize&quot;
    android:theme=&quot;@android:style/Theme.Translucent&quot; /&gt;
    &lt;/application&gt;
    
    
    &lt;/manifest&gt;
    [/code]
    
    <h2>Graddle</h2>
    And the Graddle configuration:
    
    [code lang="java"]
    apply plugin: 'com.android.application'
    
    android {
    compileSdkVersion 23
    buildToolsVersion &quot;21.1.2&quot;
    
    defaultConfig {
    applicationId &quot;com.codeandunicorns.face.doyousmile&quot;
    minSdkVersion 19
    targetSdkVersion 23
    versionCode 1
    versionName &quot;1.0&quot;
    }
    buildTypes {
    release {
    minifyEnabled false
    proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
    }
    }
    }
    
    dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile 'com.android.support:appcompat-v7:23.0.0'
    compile 'com.google.android.gms:play-services:8.1.0'
    compile 'com.google.android.gms:play-services-ads:8.1.0'
    }
    [/code]
    
    [button link="https://github.com/mitola/Do_you_smile" color="green" size="large" type="flat" shape="round" target="_self" title="" gradient_colors="|" gradient_hover_colors="|" accent_color="" accent_hover_color="" bevel_color="" border_width="1px" icon="fa-download" icon_divider="yes" icon_position="left" modal="" animation_type="0" animation_direction="down" animation_speed="0.1" alignment="center" class="" id=""]Github repository location[/button]
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
dsq_needs_sync:
  - "1"
categories:
  - ALL
  - How to
  - The Code
---
In this part of the code we are going in depth of overlays of previews and Google Vision API. The next part of the code will be properly commented so the read out should be easier

## JAVA part

<div  class="fusion-fullwidth fullwidth-box hundred-percent-fullwidth"  style='background-color: #ffffff;background-position: center center;background-repeat: no-repeat;padding-top:0px;padding-right:0px;padding-bottom:0px;padding-left:0px;'>
  <div class="fusion-builder-row fusion-row ">
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: java; title: ; notranslate" title="">
/**
 * Created by mitola on 22/08/15.
 */
public class FaceView extends View {
    private Bitmap mBitmap; // Initi of Bitmap
    private SparseArray&amp;lt;Face&amp;gt; mFaces; // And Faces

    public FaceView(Context context, AttributeSet attrs) {
        super(context, attrs);
    }

    void setContent(Bitmap bitmap, SparseArray&amp;lt;Face&amp;gt; faces) {
        mBitmap = bitmap;
        mFaces = faces;
        invalidate();
    }

    @Override
    protected void onDraw(Canvas canvas) {
        super.onDraw(canvas);
        if ((mBitmap != null) &amp;amp;&amp;amp; (mFaces != null)) {
            double scale = drawBitmap(canvas);
            drawFaceAnnotations(canvas, scale);
        }
    }

    private double drawBitmap(Canvas canvas) {
        //to draw the bitmap scaled to the device size
        double viewWidth = canvas.getWidth();
        double viewHeight = canvas.getHeight();
        double imageWidth = mBitmap.getWidth();
        double imageHeight = mBitmap.getHeight();
        double scale = Math.min(viewWidth / imageWidth, viewHeight / imageHeight);

        Rect destBounds = new Rect(0, 0, (int) (imageWidth * scale), (int) (imageHeight * scale));
        canvas.drawBitmap(mBitmap, null, destBounds, null);
        return scale;
    }

    private void drawFaceAnnotations(Canvas canvas, double scale) {
        //create paint to draw on the image
        Paint paint = new Paint();
        paint.setColor(Color.GREEN);
        paint.setStyle(Paint.Style.STROKE); //no fill
        paint.setStrokeWidth(5);

        //make a rectangle to follow with the face
        for (int i = 0; i &amp;lt; mFaces.size(); ++i) {
            Face face = mFaces.valueAt(i);
            float x1 = face.getPosition().x; //x coordinate of top left position of the face within the image
            float y1 = face.getPosition().y; //x coordinate of top left position of the face within the image
            float x2 = x1 + face.getWidth(); //width of the face region in pixels
            float y2 = y1 + face.getHeight(); //heightof the face region in pixels
            canvas.drawRoundRect(new RectF(x1 * (float) scale, y1 * (float) scale, x2 * (float) scale, y2 * (float) scale), 2, 2, paint);
        }
    }
}
</pre>
        
        <p>
          In this part you can explore the graphical overlay, which focuses mostly on making a box around the face so you know you are getting it tracked, and also used for debugging with anything you need on the screen preview. In previous testing version I was using it for example for writing smile probability value.
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: java; title: ; notranslate" title="">
/**
 * Graphic instance for rendering face position, orientation, and landmarks within an associated
 * graphic overlay view.
 */
class FaceGraphic extends GraphicOverlay.Graphic {
    private static final float FACE_POSITION_RADIUS = 10.0f;
    private static final float ID_TEXT_SIZE = 40.0f;
    private static final float ID_Y_OFFSET = 50.0f;
    private static final float ID_X_OFFSET = -50.0f;
    private static final float BOX_STROKE_WIDTH = 5.0f;
    public float smileValue = 1.0f;

    private static final int COLOR_CHOICES[] = {
        Color.BLUE,
        Color.CYAN,
        Color.GREEN,
        Color.MAGENTA,
        Color.RED,
        Color.WHITE,
        Color.YELLOW
    };
    private static int mCurrentColorIndex = 0;

    private Paint mFacePositionPaint;
    private Paint mIdPaint;
    private Paint mBoxPaint;

    private volatile Face mFace;
    private int mFaceId;

    FaceGraphic(GraphicOverlay overlay) {
        super(overlay);

        mCurrentColorIndex = (mCurrentColorIndex + 1) % COLOR_CHOICES.length;
        final int selectedColor = COLOR_CHOICES[mCurrentColorIndex];

        mFacePositionPaint = new Paint();
        mFacePositionPaint.setColor(selectedColor);

        mIdPaint = new Paint();
        mIdPaint.setColor(selectedColor);
        mIdPaint.setTextSize(ID_TEXT_SIZE);

        mBoxPaint = new Paint();
        mBoxPaint.setColor(selectedColor);
        mBoxPaint.setStyle(Paint.Style.STROKE);
        mBoxPaint.setStrokeWidth(BOX_STROKE_WIDTH);
    }

    void setId(int id) {
        mFaceId = id;
    }

    /**
     * Updates the face instance from the detection of the most recent frame.  Invalidates the
     * relevant portions of the overlay to trigger a redraw.
     */
    void updateFace(Face face) {
        mFace = face;
        postInvalidate();
    }

    /**
     * Draws the face annotations for position on the supplied canvas.
     */
    @Override
    public void draw(Canvas canvas) {
        Face face = mFace;
        if (face == null) {
            return;
        }

        // Draws a circle at the position of the detected face, with the face's track id below.
        float x = translateX(face.getPosition().x + face.getWidth() / 2);
        float y = translateY(face.getPosition().y + face.getHeight() / 2);
        canvas.drawCircle(x, y, FACE_POSITION_RADIUS, mFacePositionPaint);
        //USED FOR DEBUGGING , TODO: cleanup
        //canvas.drawText("id: " + mFaceId, x + ID_X_OFFSET, y + ID_Y_OFFSET, mIdPaint); //this can be used for extra debuging such as marking each of the faces with its own ID, rectangle
        smileValue=face.getIsSmilingProbability();
        //canvas.drawText(Float.toString(smileValue), x + ID_X_OFFSET, y + ID_Y_OFFSET*2, mIdPaint);

        /*if(smileValue &amp;gt;= 0.5f){
            canvas.drawText("YOU ARE SMILING", x + ID_X_OFFSET, y + ID_Y_OFFSET*3, mIdPaint);
        }*/

        // Draws a bounding box around the face.
        float xOffset = scaleX(face.getWidth() / 2.0f);
        float yOffset = scaleY(face.getHeight() / 2.0f);
        float left = x - xOffset;
        float top = y - yOffset;
        float right = x + xOffset;
        float bottom = y + yOffset;
        canvas.drawRect(left, top, right, bottom, mBoxPaint);
    }

    public float getSmileProbability(){
        return smileValue;
    }
}
</pre>
        
        <p>
          In the CameraSourcePreview the code is gotten from part of the samples of the Google Vision API. I think the code should be quite understandable, but if not feel free to ask questions so I can answer them and add them if needed to the blog post as well.
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: java; title: ; notranslate" title="">
public class CameraSourcePreview extends ViewGroup {
    private static final String TAG = "CameraSourcePreview";

    private Context mContext;
    private SurfaceView mSurfaceView;
    private boolean mStartRequested;
    private boolean mSurfaceAvailable;
    private CameraSource mCameraSource;

    private GraphicOverlay mOverlay;

    public CameraSourcePreview(Context context, AttributeSet attrs) {
        super(context, attrs);
        mContext = context;
        mStartRequested = false;
        mSurfaceAvailable = false;

        mSurfaceView = new SurfaceView(context);
        mSurfaceView.getHolder().addCallback(new SurfaceCallback());
        addView(mSurfaceView);
    }

    public void start(CameraSource cameraSource) throws IOException {
        if (cameraSource == null) {
            stop();
        }

        mCameraSource = cameraSource;

        if (mCameraSource != null) {
            mStartRequested = true;
            startIfReady();
        }
    }

    public void start(CameraSource cameraSource, GraphicOverlay overlay) throws IOException {
        mOverlay = overlay;
        start(cameraSource);
    }

    public void stop() {
        if (mCameraSource != null) {
            mCameraSource.stop();
        }
    }

    public void release() {
        if (mCameraSource != null) {
            mCameraSource.release();
            mCameraSource = null;
        }
    }

    private void startIfReady() throws IOException {
        if (mStartRequested &amp;amp;&amp;amp; mSurfaceAvailable) {
            mCameraSource.start(mSurfaceView.getHolder());
            if (mOverlay != null) {
                Size size = mCameraSource.getPreviewSize();
                int min = Math.min(size.getWidth(), size.getHeight());
                int max = Math.max(size.getWidth(), size.getHeight());
                if (isPortraitMode()) {
                    // Swap width and height sizes when in portrait, since it will be rotated by
                    // 90 degrees
                    mOverlay.setCameraInfo(min, max, mCameraSource.getCameraFacing());
                } else {
                    mOverlay.setCameraInfo(max, min, mCameraSource.getCameraFacing());
                }
                mOverlay.clear();
            }
            mStartRequested = false;
        }
    }

    private class SurfaceCallback implements SurfaceHolder.Callback {
        @Override
        public void surfaceCreated(SurfaceHolder surface) {
            mSurfaceAvailable = true;
            try {
                startIfReady();
            } catch (IOException e) {
                Log.e(TAG, "Could not start camera source.", e);
            }
        }

        @Override
        public void surfaceDestroyed(SurfaceHolder surface) {
            mSurfaceAvailable = false;
        }

        @Override
        public void surfaceChanged(SurfaceHolder holder, int format, int width, int height) {
        }
    }

    @Override
    protected void onLayout(boolean changed, int left, int top, int right, int bottom) {
        int width = 320;
        int height = 240;
        if (mCameraSource != null) {
            Size size = mCameraSource.getPreviewSize();
            if (size != null) {
                width = size.getWidth();
                height = size.getHeight();
            }
        }

        // Swap width and height sizes when in portrait, since it will be rotated 90 degrees
        if (isPortraitMode()) {
            int tmp = width;
            width = height;
            height = tmp;
        }

        final int layoutWidth = right - left;
        final int layoutHeight = bottom - top;

        // Computes height and width for potentially doing fit width.
        int childWidth = layoutWidth;
        int childHeight = (int)(((float) layoutWidth / (float) width) * height);

        // If height is too tall using fit width, does fit height instead.
        if (childHeight &amp;gt; layoutHeight) {
            childHeight = layoutHeight;
            childWidth = (int)(((float) layoutHeight / (float) height) * width);
        }

        for (int i = 0; i &amp;lt; getChildCount(); ++i) {
            getChildAt(i).layout(0, 0, childWidth, childHeight);
        }

        try {
            startIfReady();
        } catch (IOException e) {
            Log.e(TAG, "Could not start camera source.", e);
        }
    }

    private boolean isPortraitMode() {
        int orientation = mContext.getResources().getConfiguration().orientation;
        if (orientation == Configuration.ORIENTATION_LANDSCAPE) {
            return false;
        }
        if (orientation == Configuration.ORIENTATION_PORTRAIT) {
            return true;
        }

        Log.d(TAG, "isPortraitMode returning false by default");
        return false;
    }

    public void takeImage(){
        mCameraSource.takePicture(null, callbackPicture);
    }
    private ImageView imageView;

    CameraSource.PictureCallback callbackPicture = new CameraSource.PictureCallback(){
        public void onPictureTaken(final byte[] data)
        {
            if(mContext instanceof MainActivity) {
                MainActivity main = (MainActivity)mContext;
                main.setImageViewPicture(data);
            }
        }
    };

}
</pre>
        
        <p>
          Quite similar story goes for GraphicOverlay as well.
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: java; title: ; notranslate" title="">
/**
 * A view which renders a series of custom graphics to be overlayed on top of an associated preview
 * (i.e., the camera preview).  The creator can add graphics objects, update the objects, and remove
 * them, triggering the appropriate drawing and invalidation within the view.

 *
 * Supports scaling and mirroring of the graphics relative the camera's preview properties.  The
 * idea is that detection items are expressed in terms of a preview size, but need to be scaled up
 * to the full view size, and also mirrored in the case of the front-facing camera.

 *
 * Associated {@link Graphic} items should use the following methods to convert to view coordinates
 * for the graphics that are drawn:
 *
&amp;lt;ol&amp;gt;
 *
&amp;lt;li&amp;gt;{@link Graphic#scaleX(float)} and {@link Graphic#scaleY(float)} adjust the size of the
 * supplied value from the preview scale to the view scale.&amp;lt;/li&amp;gt;

 *
&amp;lt;li&amp;gt;{@link Graphic#translateX(float)} and {@link Graphic#translateY(float)} adjust the coordinate
 * from the preview's coordinate system to the view coordinate system.&amp;lt;/li&amp;gt;

 * &amp;lt;/ol&amp;gt;

 */
public class GraphicOverlay extends View {
    private final Object mLock = new Object();
    private int mPreviewWidth;
    private float mWidthScaleFactor = 1.0f;
    private int mPreviewHeight;
    private float mHeightScaleFactor = 1.0f;
    private int mFacing = CameraSource.CAMERA_FACING_BACK;
    private Set&amp;lt;Graphic&amp;gt; mGraphics = new HashSet&amp;lt;&amp;gt;();

    /**
     * Base class for a custom graphics object to be rendered within the graphic overlay.  Subclass
     * this and implement the {@link Graphic#draw(Canvas)} method to define the
     * graphics element.  Add instances to the overlay using {@link GraphicOverlay#add(Graphic)}.
     */
    public static abstract class Graphic {
        private GraphicOverlay mOverlay;

        public Graphic(GraphicOverlay overlay) {
            mOverlay = overlay;
        }

        /**
         * Draw the graphic on the supplied canvas.  Drawing should use the following methods to
         * convert to view coordinates for the graphics that are drawn:
         *
&amp;lt;ol&amp;gt;
         *
&amp;lt;li&amp;gt;{@link Graphic#scaleX(float)} and {@link Graphic#scaleY(float)} adjust the size of
         * the supplied value from the preview scale to the view scale.&amp;lt;/li&amp;gt;

         *
&amp;lt;li&amp;gt;{@link Graphic#translateX(float)} and {@link Graphic#translateY(float)} adjust the
         * coordinate from the preview's coordinate system to the view coordinate system.&amp;lt;/li&amp;gt;

         * &amp;lt;/ol&amp;gt;

         *
         * @param canvas drawing canvas
         */
        public abstract void draw(Canvas canvas);

        /**
         * Adjusts a horizontal value of the supplied value from the preview scale to the view
         * scale.
         */
        public float scaleX(float horizontal) {
            return horizontal * mOverlay.mWidthScaleFactor;
        }

        /**
         * Adjusts a vertical value of the supplied value from the preview scale to the view scale.
         */
        public float scaleY(float vertical) {
            return vertical * mOverlay.mHeightScaleFactor;
        }

        /**
         * Adjusts the x coordinate from the preview's coordinate system to the view coordinate
         * system.
         */
        public float translateX(float x) {
            if (mOverlay.mFacing == CameraSource.CAMERA_FACING_FRONT) {
                return mOverlay.getWidth() - scaleX(x);
            } else {
                return scaleX(x);
            }
        }

        /**
         * Adjusts the y coordinate from the preview's coordinate system to the view coordinate
         * system.
         */
        public float translateY(float y) {
            return scaleY(y);
        }

        public void postInvalidate() {
            mOverlay.postInvalidate();
        }
    }

    public GraphicOverlay(Context context, AttributeSet attrs) {
        super(context, attrs);
    }

    /**
     * Removes all graphics from the overlay.
     */
    public void clear() {
        synchronized (mLock) {
            mGraphics.clear();
        }
        postInvalidate();
    }

    /**
     * Adds a graphic to the overlay.
     */
    public void add(Graphic graphic) {
        synchronized (mLock) {
            mGraphics.add(graphic);
        }
        postInvalidate();
    }

    /**
     * Removes a graphic from the overlay.
     */
    public void remove(Graphic graphic) {
        synchronized (mLock) {
            mGraphics.remove(graphic);
        }
        postInvalidate();
    }

    /**
     * Sets the camera attributes for size and facing direction, which informs how to transform
     * image coordinates later.
     */
    public void setCameraInfo(int previewWidth, int previewHeight, int facing) {
        synchronized (mLock) {
            mPreviewWidth = previewWidth;
            mPreviewHeight = previewHeight;
            mFacing = facing;
        }
        postInvalidate();
    }

    /**
     * Draws the overlay with its associated graphic objects.
     */
    @Override
    protected void onDraw(Canvas canvas) {
        super.onDraw(canvas);

        synchronized (mLock) {
            if ((mPreviewWidth != 0) &amp;amp;&amp;amp; (mPreviewHeight != 0)) {
                mWidthScaleFactor = (float) canvas.getWidth() / (float) mPreviewWidth;
                mHeightScaleFactor = (float) canvas.getHeight() / (float) mPreviewHeight;
            }

            for (Graphic graphic : mGraphics) {
                graphic.draw(canvas);
            }
        }
    }
}
</pre>
        
        <p>
          XML files
        </p>
        
        <p>
          And the only thing left now is the XML files such as a description of design and strings.xml file. There is also the Manifest, but I think the most important part is the application part which I am also adding at the end. Together with the Github url where you can access all the source code for this Google Vision API example.
        </p>
        
        <h2>
          Activity_main
        </h2>
        
        <p>
          This file is called activity_main.xml
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: xml; title: ; notranslate" title="">
&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;RelativeLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/topLayout"
    android:orientation="vertical"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:columnCount="2"
    android:rowCount="2"
    xmlns:ads="http://schemas.android.com/apk/res-auto"
    android:keepScreenOn="true"&gt;

    &lt;com.codeandunicorns.face.doyousmile.uicamera.CameraSourcePreview
        android:id="@+id/preview"
        android:layout_width="208dp"
        android:layout_height="277dp"
        android:layout_gravity="center|left|top"&gt;

    &lt;/com.codeandunicorns.face.doyousmile.uicamera.CameraSourcePreview&gt;

    &lt;ImageView
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:id="@+id/imageView"
        android:layout_gravity="center_horizontal|left|top"
        android:layout_alignParentTop="true"
        android:layout_alignParentEnd="true"
        android:layout_above="@+id/jokeView"
        android:layout_toEndOf="@+id/preview" /&gt;

    &lt;com.codeandunicorns.face.doyousmile.uicamera.GraphicOverlay
        android:id="@+id/faceOverlay"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_alignParentTop="true"
        android:layout_alignParentStart="true"
        android:layout_above="@+id/jokeView"
        android:layout_toStartOf="@+id/imageView" /&gt;

    &lt;LinearLayout
        android:orientation="vertical"
        android:layout_width="match_parent"
        android:layout_height="110dp"
        android:layout_gravity="bottom"
        android:layout_alignParentBottom="true"
        android:layout_alignParentStart="true"
        android:id="@+id/linearLayout"
        android:gravity="center_horizontal"
        android:weightSum="1"&gt;

        &lt;Button
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="@string/button_main"
            android:id="@+id/takepicturebutton"
            android:textSize="20sp" /&gt;

        &lt;com.google.android.gms.ads.AdView
            android:id="@+id/adView"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            ads:adSize="BANNER"
            ads:adUnitId="@string/banner_ad_unit_id"&gt;
        &lt;/com.google.android.gms.ads.AdView&gt;

    &lt;/LinearLayout&gt;

    &lt;TextView
        android:layout_width="fill_parent"
        android:layout_height="fill_parent"
        android:text="@string/starting_text"
        android:id="@+id/jokeView"
        android:layout_gravity="right|top"
        android:layout_below="@+id/preview"
        android:layout_above="@+id/linearLayout"
        android:textSize="17dp"
        android:textIsSelectable="false"
        android:paddingEnd="10dp"
        android:paddingStart="10dp" /&gt;


&lt;/RelativeLayout&gt;
</pre>
        
        <h2>
          Strings.xml
        </h2>
        
        <p>
          This file is called strings.xml:
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: xml; title: ; notranslate" title="">
&lt;resources&gt;
    &lt;string name="app_name"&gt;Do you smile?&lt;/string&gt;

    &lt;string name="hello_world"&gt;Hello world!&lt;/string&gt;
    &lt;string name="action_settings"&gt;Settings&lt;/string&gt;
    &lt;string name="banner_ad_unit_id"&gt;ca-app-pub-YOURID&lt;/string&gt;
    &lt;string name="starting_text"&gt;Scan your current mood! Do you smile or not is the question?\nClick and find out!&lt;/string&gt;
    &lt;string name="button_main"&gt;Take mood picture&lt;/string&gt;
&lt;/resources&gt;
</pre>
        
        <h2>
          AndroidManifest.xml
        </h2>
        
        <p>
          And the AndroidManifest.xml file contents with permissions etc:
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: xml; title: ; notranslate" title="">
&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.codeandunicorns.face.doyousmile" &gt;

    &lt;uses-feature android:name="android.hardware.camera" /&gt;

    &lt;uses-permission android:name="android.permission.CAMERA" /&gt;

    &lt;application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:theme="@style/AppTheme"&gt;
        &lt;meta-data android:name="com.google.android.gms.version"
            android:value="@integer/google_play_services_version" /&gt;
        &lt;activity
            android:name=".MainActivity"
            android:label="@string/app_name" &gt;
            &lt;intent-filter&gt;
                &lt;action android:name="android.intent.action.MAIN" /&gt;

                &lt;category android:name="android.intent.category.LAUNCHER" /&gt;
            &lt;/intent-filter&gt;
        &lt;/activity&gt;
        &lt;meta-data
            android:name="com.google.android.gms.vision.DEPENDENCIES"
            android:value="face" /&gt;
        &lt;activity android:name="com.google.android.gms.ads.AdActivity"
            android:configChanges="keyboard|keyboardHidden|orientation|screenLayout|uiMode|screenSize|smallestScreenSize"
            android:theme="@android:style/Theme.Translucent" /&gt;
    &lt;/application&gt;


&lt;/manifest&gt;
</pre>
        
        <h2>
          Graddle
        </h2>
        
        <p>
          And the Graddle configuration:
        </p>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
    
    <div  class="fusion-layout-column fusion_builder_column fusion_builder_column_1_1  fusion-one-full fusion-column-first fusion-column-last fusion-column-no-min-height 1_1"  style='margin-top:0px;margin-bottom:0px;'>
      <div class="fusion-column-wrapper" style="background-position:left top;background-repeat:no-repeat;-webkit-background-size:cover;-moz-background-size:cover;-o-background-size:cover;background-size:cover;"  data-bg-url="">
        <pre class="brush: java; title: ; notranslate" title="">
apply plugin: 'com.android.application'

android {
    compileSdkVersion 23
    buildToolsVersion "21.1.2"

    defaultConfig {
        applicationId "com.codeandunicorns.face.doyousmile"
        minSdkVersion 19
        targetSdkVersion 23
        versionCode 1
        versionName "1.0"
    }
    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }
}

dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile 'com.android.support:appcompat-v7:23.0.0'
    compile 'com.google.android.gms:play-services:8.1.0'
    compile 'com.google.android.gms:play-services-ads:8.1.0'
}
</pre>
        
        <div class="fusion-button-wrapper fusion-aligncenter">
          <a class="fusion-button button-flat fusion-button-round button-large button-green button-2" target="_self" href="https://github.com/mitola/Do_you_smile"><span class="fusion-button-icon-divider button-icon-divider-left"><i class="fa fa-download"></i></span><span class="fusion-button-text fusion-button-text-left">Github repository location</span></a>
        </div>
        
        <div class="fusion-clearfix">
        </div>
      </div>
    </div>
  </div>
</div>