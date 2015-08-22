# Appngage
Integration Steps for Appngage

##Appngage

Introduction: Appngage is a User Engagement and Growth Hack tool kit for Mobile Apps.

Engage and Retain Multiple solutions to increase engagement of your app's users, along with A/B testing abilities.!

It helps app developers to engage users effectively without any coding.

###Integration Steps:

Appngage uses GCM (Google Cloud Messaging) for push messages so it is only compatible with Google Play.

###There are two steps to getting it up and running:

1.	Set up your Google Developer project to get your Authorization key and GCM Sender Id.

2.	Implement Appngage Push in your app.

###Setting up your Google Developer project

The Appngage dashboard needs to have your authorization key to be able to push to users of your application and you'll need your GCM Sender ID to place within your app code.

###STEP 1 : 
Creating a new Google API Project

Go to the Google Developers Console: https://console.developers.google.com/project

Create a new project

![Alt text](https://github.com/Espertosys-Labs-Pvt-Ltd/Appngage/blob/master/images/step1.jpg?raw=true "Optional Title")

###STEP 2 :
Getting your GCM Sender ID

![Alt text](https://github.com/Espertosys-Labs-Pvt-Ltd/Appngage/blob/master/images/step2.jpg?raw=true "Optional Title")

###STEP 3 :
Activating GCM API

Go to the API & Auth menu and select APIs. Then look for the Google Cloud Messaging for Android line and click on the OFF button to activate it:

![Alt text](https://github.com/Espertosys-Labs-Pvt-Ltd/Appngage/blob/master/images/step3.jpg?raw=true "Optional Title")

Go to your newly created project and get your Project Number at the top of the page

###STEP 4 
Getting your Authorization key

   1 . Go to Credentials and click Create new Key:

   ![Alt text](https://github.com/Espertosys-Labs-Pvt-Ltd/Appngage/blob/master/images/step4.jpg?raw=true "Optional Title")

   2 .Select Server key, and click Create:

   ![Alt text](https://github.com/Espertosys-Labs-Pvt-Ltd/Appngage/blob/master/images/step5.jpg?raw=true "Optional Title")

That's it; you should now see your Authorization key that you need to provide to Appngage:

![Alt text](https://github.com/Espertosys-Labs-Pvt-Ltd/Appngage/blob/master/images/step6.jpg?raw=true "Optional Title")

###STEP 5 :
Setting up your application

At this point you should have:

Your GCM Sender ID (e.g. 187119303295)
Your Google Authorization Key (e.g. AIzaSyABaO6Pjb_4XHhYfMqSNVKlw41GCC3d6pw)
You will need to input the GCM Sender ID below in the config file of Appngege. The Google authorization key is not used in code, 
but needs to be placed within your app's settings page on the Appngage dashboard.


###STEP 6 :
Configure your AndroidManifest.xml

Add the following lines to your AndroidManifest.xml within the <manifest...>


<manifest...>

   <uses-sdk android:minSdkVersion="8" android:targetSdkVersion="19" />

    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />  
    <!-- Optional permissions. GET_ACCOUNTS is used to pre-populate customer's email in form fields. -->
    <uses-permission android:name="android.permission.GET_ACCOUNTS" />
    <!-- Optional permissions. WRITE_EXTERNAL_STORAGE is used to improve the performance by storing campaign images. -->
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />

1. Create an App in our dashboard. Link: [https://dashboard.appngage.com](https://dashboard.appngage.com)

2. Download SDK:

Appngage SDK source for Android Studio can be downloaded from [Here](https://dashboard.appngage.com/documentation), this includes test App.


###STEP 6 :
Initializing the Appngage SDK

1)  Initialize the Appngage SDK by calling 
mAppngage.getInstance()
 mAppngage = NgageManager.getInstance(this);
        mAppngage.requestGcmRegistrationId(this);
        mAppngage.setOnline();
   in onCreate() method of your application Main Activity class.
   
2)  For further customization, call any of these methods.
setUserId(String userId); // If you would like to pass your App's user ID as a unique identifier. If not called, a screen will be prompted asking User's name.
setHeaderColor(int color); //Theme color according to your app.
setDarkTitle(Boolean isDark);// If theme color is on the lighter side.
Alright!
We're set to take Off.

