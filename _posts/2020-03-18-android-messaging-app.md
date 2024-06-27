---
layout: post
title: "YThis - Android messaging app"
date: 2020-03-01
categories: projects
githubRepo : 'https://github.com/nagendar-pm/YThis_Android_Chatapp/blob/master/'
rawParam : '?raw=true'
---

YThis or **Why this**? Programmers never really come up with good names and I too suffer with the same conditiion it seems. This is an android messaging platform built to learn multiple areas in Android. 

<!--more-->

My primary areas of interest in building this application were learning:
1. Authentication & Authorization
2. Databases
3. Android UI


This is a Chat-app made for Android Operating System, using the IDE Android
Studio. This project is built with the programming language Java and includes
certain other tools like XML for the layout of different Activities of the App.
This app is basically a mini Whatsapp clone.

On successful installation of this app, you can see an Activity like this as shown
in the [Main Activity](#main-activity) image.

<a id="main-activity"></a>

![Main Activity]({{ page.githubRepo }}resources/main-activity-img-portrait.png{{ page.rawParam }})
*Main Activity*

Here you can login or register, if you have done or haven’t done any registration
into the app respectively. You can look at those activities in [Registration and Login image](#registration-activity) respectively.

Authentication of users is based on e-mail id and on successful registration with
your mail-id, if it is not already registered prior, you will get a confirmation
mail through which you can login. If the mail-id already exists, you will get a
toast saying, "You can’t register with this email". During Login, if you forgot
the password, you can reset the password using your registered mail address, as
shown in the [Reset Password Activity](#reset-password-activity)

<a id="registration-activity"></a>
![Registration Activity]({{ page.githubRepo }}resources/registration-activity-img-portrait.png{{ page.rawParam }})
*Registration Activity*

![Login Activity]({{ page.githubRepo }}resources/login-activity-img-portrait.png{{ page.rawParam }})
*Login Activity*

<a id="reset-password-activity"></a>
![Reset Password Activity]({{ page.githubRepo }}resources/reset-password-activity-img-portrait.png{{ page.rawParam }})
*Reset Password Activity*

On successful login into the app, you can see the list of users who are already
logged in into the app as shown in the [User Activity image](#users-activity). If the profile picture of the
user has a green colored dot at the bottom right, it means the user is active and
using the app now. If the dot is gray, it means that the user is offline as shown.
You can chat with any user, whom you can see in your users list. On pressing
any User, you can see a view similar to the [Chat Activity image](#chat-activity).

<a id="users-activity"></a>

![User Activity]({{ page.githubRepo }}resources/users-activity-img-portrait.png{{ page.rawParam }})
*User Activity*

<a id="chat-activity"></a>
![Chat Activity]({{ page.githubRepo }}resources/chat-activity-img-portrait.png{{ page.rawParam }})*Chat Activity*

You can also edit your profile picture, by clicking on the camera icon at the
bottom right of the picture, which opens your gallery and asks you to select an
image as shown in the [Profile Activity image](#profile-activity).

<a id="profile-activity"></a>
![Profile Activity]({{ page.githubRepo }}resources/profile-activity-img-portrait.png{{ page.rawParam }})
*Profile Activity*