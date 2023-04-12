---
title: "WTB!! What The Bug..."
datePublished: Fri Mar 10 2023 20:40:24 GMT+0000 (Coordinated Universal Time)
cuid: clf4fr5st00090ajjevg5cf0a
slug: wtb-what-the-bug
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1678566662755/09314cc4-11e8-484c-b159-476e744fcad0.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1678567351311/93375d51-377f-477d-8c61-07ff21d65500.png
tags: android, hashnode, debuggingfeb, debuggingfeb-writeathon

---

## Introduction

This is not an extreme-level debugging story where people debug their Dapr API applications with Rider or solve some kind of ML hyperparameter tuning issues.

I consider myself a "newly intermediate" kind of developer who has bugs all the time as a supporting partner.

The bug doesn't care whether you're a freshy or an intermediate like me or the pro one. It finds its way to enter your life as ants do with sugar.

Just place some sugar openly anywhere in the world, and don't know from where the ants will reach there from nowhere.

It's the same with writing the code and bugs will appear from nowhere. It can be just a small " ; " semicolon or a big server connecting error. So all developers must know how to handle the bugs with care.

Here are one of my(first encounter) debugging experiences:

## My first-ever project

If you have read my 2022 journey then you know that I was very fond of the applications like how they are made, and how they work. So I decided to learn android development and wanted to make my own application. This is my first ever project also in my tech career.

So I started learning android development from a random platform.

Their course structure is like one app they'll make up for you and you follow them and then one app they'll leave for you with some hints. I made an app called BookHub. Basically just followed the instructions and made with them accordingly.

Then I started with another one that they gave as an assignment app called the FoodRunner application. The app must have a signup page than a page must open up with all the restaurant's list and that's it.

It was going smoothly at the beginning.

I made a welcome page

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678558386037/aa1138c9-a638-4779-bc2d-434a3fdfc8de.png align="center")

and then the signup page easily

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678559054079/4c17ed94-1f74-4468-96e2-055baf87036e.jpeg align="center")

and then the login page smoothly which lands on another page that has a dashboard.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678559381384/cc319d41-cdc6-4044-a0b5-0410d96260c6.jpeg align="center")

## Main issue

The problem arose when the main page opens up, it was not showing the list of restaurants, just a blank page with a toast message that is on the try-catch block.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678556961193/7c9fb7d6-a430-4b4e-9c38-504df7240c55.png align="center")

This is my try-catch block code in which the toast message "Some Error Occurred!!!" was appearing.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678564762906/c21047ee-3595-4df6-89f2-28638043d9f0.png align="center")

I didn't take the screenshot that time of my error page. The error was obviously with the JSONObject and GET methods.

## Steps I followed to debug

I. I checked the hints that they gave with the instructions and that didn't help much.

II. I checked the key names because data extracted from the JSON Object must match as they are case-sensitive.

III. Also checked the data types because sometimes mistakes like getString() instead of getInt() can put you in trouble.

IV. Then I just copy pasted my error and searched randomly on google and definitely got no help.

V. Then I went to stack overflow (all the devs visited at some point of debugging). There are a lot of developers who posted not the exact but kind of same error. I tried them a lot and spent months searching on stack overflow because I thought that this is the last option from where help can be found.

And that too didn't help me.

As I was not aware of an open community where folks are there to help people like us.

Then I left my first ever android project in between due to the error and ended my course and got depressed and started thinking that maybe these coding and development things are not my cup of tea.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678564853915/97ec8cef-9371-4a73-ad80-ff51d573caa2.png align="left")

A whole year passed away......

Suddenly a notification popped up from where I was learning android. With the same error that I was facing with my project, someone also posted there. Basically, they created a channel where all the learners can interact but that's not very active. Just a lost kind of channel.

So I saw that message then I messaged them personally. Then we discussed the error and exchanged our codes and matched line by line and we both started correcting our code.

## Magical Moment

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678564943185/5dc7c1ab-d618-495a-8ae3-10361f0f90c7.png align="center")

And then magic happened, that application is running for both. I can't express my feelings when I saw my application running, that was something else, like out of the world feeling.

The list of restaurants is showing now!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678561174561/b005f954-c9a8-47bf-b4cd-8cb2d07483f3.jpeg align="center")

## Things you can learn from my mistakes💡

* Use break points: I didn't check my source code and ran without debugging at necessary breaking points.
    
    Always debug where it needs to be so that you can catch your error at that particular point rather than finding it in the whole code base.
    

> Breakers save you, plane roads can cause accidents!!

* Understand the issue: When my error appeared instead of reading and understanding the error message I started randomly searching with the keynote.
    
    First, try to understand what your error is saying then jump for searching.
    

> First, understand then execute.

* Communicate: When nothing worked, I quit my project. Don't do this. This will lead to your confidence being down badly. There are a lot of amazing communities out there where you can get help easily.
    

> Be vocal, learn in public, share what you are learning, share the issue where you are stuck, and you will definitely get help.

* AI Checker: Nowadays there are a lot of OpenAI tools where you can get your errors resolved.
    
    In my case, I can use a JSON validator to detect my error done and dusted.
    
    You know what I'm gonna talk about now. Yes, OpenAI Chatgpt, is something everyone is talking about and I'm too using this quite oftenly.
    
    It can help you to get your error cleared. You just need to talk with them as you're explaining to your friend and this will give you solutions.
    
* Communities: Join the great communities, and get in touch with the same kind of folks with a similar tech stack. This will help you insanely in your good-bad times.
    

---

This blog is written for the #DebuggingFeb Writeathon organized by Hashnode itself. I am thankful to them for giving such amazing opportunities to write and share. If you enjoyed my debugging experience give it a ❤️.

Thanks for reading!❣️