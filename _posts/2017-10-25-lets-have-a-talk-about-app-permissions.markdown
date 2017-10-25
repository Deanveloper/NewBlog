---
layout: post
title: "Let's Have a Talk About App Permissions"
date: "2017-10-25 12:27:23 -0400"
---
Not long ago, I saw [this tweet][the tweet]. It got me thinking, do people really not know the purpose in App permissions? I've always been careful with app permissions, I don't want Facebook using my microphone in the background while I have the app open.

After all, we give apps permissions all the time. It makes sense to give Twitter permission to my photos, I wanted to tweet out the awesome selfie I took! But now Twitter has access to *all* of my photos, not just the one I wanted to share.

Just as a bit of a scare, let's go over everything that an app can do when it gets certain permissions.

* Camera Access (as listed as the example in the tweet)
  * Access to record you or what you're looking at whenever the app is running
  * Access to upload taken pictures wherever they want without your knowledge
  * Run scans on said images with facial recognition
  * Figure out your current mood based on facial recognition
* Photo Access
  * Access to all of your photos
  * Access to upload every one of your photos/videos
  * Access to scan photos with facial recognition
  * Access to photo metadata, **including where the photo was taken**
  * Get basic information such as where the user lives through data analysis with photo location
* Microphone Access
  * Access to your microphone while the app is running
  * Record any conversations you have while the app is running
  * Run speech-to-text software on conversations you have
* Location Access
  * Access your current location
  * Access to tell if you are home or not (after some data analysis)
  * Figure out where you work or go to school
  * Figure out your approximate speed
  * Depending on the level of access, all of these even when the app is **not in use**
* Twitter/Facebook Access
  * Access to the name of your Facebook/Twitter accounts
  * Access to gather information from your Facebook/Twitter accounts (depending on Facebook/Twitter privacy settings)
    * Your name
    * Your mother's name
    * Your mother's parent's last name (aka _your mother's maiden name_)
    * Your SO's name
    * Your job, education, etc
    * Your friends' names
    * Your preferences
    * Your friends' preferences
    * Your photos/videos
* Contact Access
  * Access to view all of your contacts
  * Access the contact information of your contacts
  * The ability to _contact_ your contacts
  * Collect information on your friends based on your (and other people who have your friends as contacts) preferences
* HomeKit Access
  * Access to turn on/off lights
  * Access to turning heat up/down
  * Access to unlock your front door
  * This is just all-around bad
* Accelerometer (gyro) Access
  * All apps can use this **without asking the user**
  * Even [web apps][what the user is doing] can use this without asking
  * Through data analysis with the accelerometer, the app can tell vaguely as to what the user is doing.

So now comes the question, how do we limit app's access to such services, without limiting what we want them to do? After all, it's really convenient to be able to take pictures inside of Facebook and instantly share them, I just don't want them taking pictures whenever they want.

1. Use built-in apps which do not have permissions associated with them
  * This is convenient for the user as they don't need to answer yet another pop-up.
  * Allows access for a built-in camera app which only takes pictures when the user wants to.
  * Allows access to select a single contact (or group of contacts) through a built-in app.
  * Similar things for stuff like photos, microphone, etc.
  * Perhaps even let the app provide a custom format for the camera/photos/whatever app.
2. Temporary permissions
  * Allow access for some amount of time, rather than once-and-forever.
  * Could also be for the current session (revoke permission when user exits the app).
  * ie: Allow Google Maps to use my location (even in the background) for a few minutes/hours.
  * Give access for the app to request more time from the user if needed.
3. Warn the user
  * Tell the user what the app can do with the permissions it wants.
  * Of course don't go into the detail like I did earlier, just something along the lines of "can take photos whenever it wants while using the app" (with better wording of course).

# Conclusion
Apps can do more than what the user wants to do with given permissions. While you might want to just take a picture for your new Facebook profile picture, Facebook now has permissions to take pictures whenever it wants, as long as the app is open. [Ever used Facebook on the toilet][the tweet]?

[the tweet]: https://twitter.com/KrauseFx/status/923210131889942528
[what the user is doing]: https://github.com/KrauseFx/whats-the-user-doing
