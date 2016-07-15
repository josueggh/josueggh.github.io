---
layout: post
title: Device Orientation and Firebase
subtitle: Using the Device Orientation and Firebase I built an interactive web between your mobile and a monitor of the devices connected  
categories: [chrome, javascript, firebase, post]
fb-img: http://josueggh.com//img/post/deviceorientation.jpg
---

As web developer after see the interactive activities before the start of the previous Google I/O as 
[Paper Planes](https://paperplanes.withgoogle.com/){:target="_blank"} where the user using Google Chrome in their 
own smart phone could interact with the other assistants in a huge screen, all this by only changing the orientation and position
 of the phone, so born in my the curiosity to create a project that involves some of this characteristics.
 
 The idea of the project is simple, changing the orientation of the phone in any of their axis will change the 
 background of a webpage and all the devices will be capable to be displayed into one screen with their current color.
 
### 1.- Device orientation, getting the color.

The [Device Orientation event specification](https://w3c.github.io/deviceorientation/spec-source-orientation.html){:target="_blank"}
  mention that we can get the value of the different tilt angles of our devices, and this values will be living in the 
  *alpha*, *beta* and *gamma* properties.
  
<img src="/img/post/deviceorientation.jpg" title="Device Orientation">
  
  - **Alpha:** is the compass direction where the device is facing
  - **Beta:** is the front-to-back tilt (front is positive)
  - **Gamma:** is the left-to-right tilt (right is positive)
  
By lucky, the RGB color system has 3 variables, so the idea is use this angle values and map them into a 
range from 0 to 255. With the next code our web page will be able to change the background each time we move our device.

<script src="https://gist.github.com/josueggh/aa34eccb55cb8ced2297e969eb47c9d5.js"></script>

### 2.- How test it in Chrome.

So, how we can test the code? Actually, we have two way to do it.

The **first** option is using the 
*[Device Orientation Emulator](https://developers.google.com/web/tools/chrome-devtools/iterate/device-mode/device-input-and-sensors){:target="_blank"}* 
in *Chrome Devtools*, this option is avaiable under the "*More tools*" menu, after that you'll have a space where you could manipulate the orientation of a device.   

<img src="/img/post/chrometools.jpg" title="Device Orientation Emulator">

With the emulator open and active, now you'll be able to see how the background property change on the *body* tag.
<div style="text-align:center;">
<img src="/img/post/emulator.gif">
</div>

The **second** option is "*Inspect devices*", to do that you need an Android 4.2 or later and enable the USB debugging, to
know more about this option you can follow the next link: [Remote Debugging Android Devices](https://developers.google.com/web/tools/chrome-devtools/debug/remote-debugging/remote-debugging).

In my case I'm using Webstorm to run directly the HTML, so the port assigned to the web is 63342, so the first step is 
create the rule for the port forwarding as follows (I' want to redirect it to 8080 port).

<div style="text-align:center;">
<img src="/img/post/forward.jpg" style="width:350px">
</div>

After that I'll be able to open the localhost:8080 directly on the phone and display the web page running in the localhost of 
my machine.

<div style="text-align:center;">
<img src="/img/post/sendphone.jpg" style="width:384px">
</div>

Indeed if we click under the "*Inspect*" button in this panel, Chrome will open another window where we can debug in real
  time what is happening with our phone, in the this case if we move it, this window will reflect the same color that we 
   have in the phone. 
   
This way of debug it's really helpful when we would to see what is happening in our devices, also if we modified something
in this windows it will be reflected in our phone.

<div style="text-align:center;">
<img src="/img/post/phone.jpg" style="width:350px">
</div>

### 3.- Firebase as our main connector.

So, what's next, now we have the part that change our background, we need to send this information to Firebase to build a 
real time application, we're going to use Firebase 3.x, at the same way as the Legacy version, we would include a login to 
identify each user and also we're going to detect the *disconnect* status to delete the object into our database. 

<script src="https://gist.github.com/josueggh/930355859b85b63eb6afef57aeadfca1.js"></script>

You can look the final result of the application in [https://devicemotion.firebaseapp.com/](https://devicemotion.firebaseapp.com/){:target="_blank"},
I strongly recommend you try it on your **smart phone**.

### 4.- Creating our monitor system.

<div style="text-align:center;">
<img src="/img/post/colors.gif" style="width:300px">
</div>

Finally, we are going to connect to our Firebase database to create the devices monitor, showing the current users moving
 their devices and the current background color. 
 
For that we're going to use the change state of Firebase to create, destroy and update DIVs.

<script src="https://gist.github.com/josueggh/10d324a219da6db6b9fbd5ee796537a8.js"></script>

If you're connected in the application, you can find you in the next link [https://devicemotion.firebaseapp.com/monitor/](https://devicemotion.firebaseapp.com/monitor/){:target="_blank"}
the full code is available via Github in the next repository: [https://github.com/josueggh/deviceorientation](https://github.com/josueggh/deviceorientation){:target="_blank"}
, all the feedback is welcome.