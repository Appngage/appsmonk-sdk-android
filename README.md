# Appsmonk

Introduction: Appngage is a User Engagement and Growth Hack tool kit for Mobile Apps.

Engage and Retain Multiple solutions to increase engagement of your app's users, along with A/B testing abilities.!

It helps app developers to engage users effectively without any coding.

##Integration Steps:

Appngage uses GCM (Google Cloud Messaging) for push messages so it is only compatible with Google Play.

###There are two steps to getting it up and running:

1.	Set up your Google Developer project to get your Authorization key and GCM Sender Id.

2.	Implement Appngage Push in your app.

###Setting up Google Developer project

The Appngage dashboard needs to have your authorization key to be able to push to users of your application and you'll need your GCM Sender ID to place within your app code.

###STEP 1 : Creating a new Google API Project

Go to the Google Developers Console: https://console.developers.google.com/project

Create a new project

![Alt text](https://github.com/Appngage/appngage-sdk-integration/blob/master/image/step1.png?raw=true "Optional Title")

###STEP 2 : Getting your GCM Sender ID

![Alt text](https://github.com/Appngage/appngage-sdk-integration/blob/master/image/step2.png?raw=true "Optional Title")

###STEP 3 : Activating GCM API

Go to the API & Auth menu and select APIs. Then look for the Google Cloud Messaging for Android line and click on the OFF button to activate it:

![Alt text](https://github.com/Appngage/appngage-sdk-integration/blob/master/image/step3.png?raw=true "Optional Title")

![Alt text](https://github.com/Appngage/appngage-sdk-integration/blob/master/image/step4.png?raw=true "Optional Title")

Go to your newly created project and get your Project Number at the top of the page

###STEP 4 : Getting your Authorization key

   1 . Go to Credentials and click Create new Key:

   ![Alt text](https://github.com/Appngage/appngage-sdk-integration/blob/master/image/step5.png?raw=true "Optional Title")
   
   ![Alt text](https://github.com/Appngage/appngage-sdk-integration/blob/master/image/step6.png?raw=true "Optional Title")

   2 .Select Server key, and click Create:

   ![Alt text](https://github.com/Appngage/appngage-sdk-integration/blob/master/image/step7.png?raw=true "Optional Title")
   

That's it; you should now see your Authorization key that you need to provide to Appngage:

![Alt text](https://github.com/Appngage/appngage-sdk-integration/blob/master/image/step8.png?raw=true "Optional Title")


###Setting up your application

At this point you should have:

Your GCM Sender ID (e.g. 458299266933)
Your Google Authorization Key (e.g. AIzaSyBVu_T1V6q1l3JAXqx3fmCgwPslRHThx3g)
You will need to input the GCM Sender ID below in the config file of Appngege. The Google authorization key is not used in code, 
but needs to be placed within your app's settings page on the Appngage dashboard.

###Here are the steps to create an app in our dashboard.

1) Go to Link: [https://appngage.com](https://appngage.com) and request access.

2) We will send an email with the registration link to appngage dashboard

3) Follow the link and Register.

4) Click on 'Add an app' button to add the app and enter your GCM Server API Key and click on 'save'.

You will get the Appngage API key once you save the App and you can see the same under 'settings tab'.

###Initializing Appngage SDK With Android Studio

Here are the steps:
<pre>
Be sure to replace <b>YOUR.PACKAGE</b> with your actual package name, for example: <b>com.google.android</b>
Make sure you are connected to network during the integration.
</pre>

1)  Configure your App build.gradle file:
   
   a) Add the following line under the dependencies section.
   ```
   compile 'com.appngage:gcm:0.3.6'
   ```
   b) Add the following line under the defaultConfig section
   ```
   multiDexEnabled true
   ```
2)  Configure your AndroidManifest.xml

  a) Add the following lines in AndroidManifest.xml file
```xml
    <uses-permission android:name="android.permission.INTERNET" /> //(Ignore if already included in your App)
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" /> //(Ignore if already included in your App)
    <permission android:name="YOUR.PACKAGE.permission.C2D_MESSAGE" android:protectionLevel="signature" />  //(Ignore if
    already included in your App)
    <uses-permission android:name="YOUR.PACKAGE.permission.C2D_MESSAGE" />  //(Ignore if already included in your App)
```
   b) Add the following lines at the end under application tag in AndroidManifest.xml file. 
```xml
    <meta-data
    android:name="appngage_id"
    android:value="@string/appngage_id"></meta-data>
    
    <meta-data
    android:name="gcm_sender_id"
    android:value="@string/gcm_sender_id"></meta-data>
   
    <meta-data
    android:name="gcm_launching_activity"
    android:value="YOUR.PACKAGE.YOUR_LAUNCHING_ACTIVITY"></meta-data>
    
```
   <pre>
   Be sure to replace <b>YOUR_LAUNCHING_ACTIVITY</b> with your actual <b>LAUNCHING ACTIVITY</b>
   </pre>
   
3) Add the following lines in res/values/stings.xml file
```xml
    <string name="appngage_id">YOUR_APPNGAGE_API_KEY</string>
    <string name="gcm_sender_id">YOUR_GCM_SENDER_ID</string>
 ```
 <pre>
 Be sure to replace <b>YOUR_APPNGAGE_APT_KEY</b> with your actual <b>APPNGAGE API KEY</b> from Appngage Dashboard.
 Also replace <b>YOUR_GCM_SENDER_ID</b> with your actual <b>GCM SENDER ID</b> that you obtained earlier.</pre>
 
4)Configure Push and In App Chat

Finally after the above steps are done, 

Add the following lines in the your launching activity file.
Below shown is a sample code of the Launching Activity file.
```java
   import com.appngage.api.NgageManager;
   import com.appngage.gcm.dto.GCMItem;
   
   public class MainActivity extends ActionBarActivity implements View.OnClickListener {
       private Button button;
       private NgageManager mAppngage;
       @Override
       protected void onCreate(Bundle savedInstanceState) {
           super.onCreate(savedInstanceState);
           setContentView(R.layout.activity_main);
           button = (Button) findViewById(R.id.in_app_message_button);
           button.setOnClickListener(this);
           mAppngage = NgageManager.getInstance(this);
           try {
               mAppngage.setUserFirstName("TestFnamee")
                       .setUserPhoneNumber("123456987")
                       .setUserEmailId("test@test.com")
                       .initManager(this);
           } catch (AppngageException e) {
               e.printStackTrace();
           }
          onHandleIntent(getIntent());
       }
       
   private void onHandleIntent(Intent intent) {
        //Check if the push is from Appngage
        if (mAppngage.isFromAppNgage(intent)) {
            GCMItem gcmItem = mAppngage.getGCMItem(intent);
        } else {
            //Handle your custom push here...
        }
    }
    
   @Override
    protected void onNewIntent(Intent intent) {
        super.onNewIntent(intent);
        onHandleIntent(intent);
    }
    
   @Override
   public void onClick(View view) {
       mAppngage.startChat();
      }
      
      @Override
    protected void onStart() {
        super.onStart();
        // Call below method when your application opens.
        mAppngage.onOpenApplication();
    }

    @Override
    protected void onStop() {
        super.onStop();
        // Call below method when your application exits.
        mAppngage.onCloseApplication();
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        // Call below method when application exits - Mandatory
        mAppngage.clear();
    }
   }
```
Here, the button refers to the button in your app which you would want to lead to Chat Support.

5)  For further customization, call any of these methods in the onCreate() method of your launch activity.
```java
HashMap<String, String> attributes = new HashMap<String, String>();
attributes.put("Category", "Sports");
attributes.put("Rated", "5 Stars");
try {
   mAppngage.setCustomAttributes(this,attributes); //Optional. Set any custom properties/attribute specific to your app.
   mAppngage.sendCustomEvent("Browsed Samsung Galaxy SM-G920IZDAINS Phone");
   mAppngage.setUserId("ANY_STRING_OR_USERID"); // If you would like to pass your App's user ID as a unique identifier. If not called, a screen will be prompted asking User's name.
   mAppngage.setHeaderColor(Color.parseColor("#COLOR_CODE")); //Theme color according to your app.
   mAppngage.setDarkTitle(Boolean isDark);// If theme color is on the lighter side.
   mAppngage.setVibration(this,true); //Optional. Set if you need the notification vibration.
   mAppngage.setNotificationTone(this,"Path to .mp3 file"); //Optional. Set if you need the notification tone.
} catch (AppngageException e) {
   e.printStackTrace();
}

```
Alright!

We're set to take Off.

