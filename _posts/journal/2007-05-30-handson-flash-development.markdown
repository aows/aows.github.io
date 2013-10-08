---
layout: post
title:  "Hands on Flash development for the first time"
date:   2007-05-30 16:01:48
categories: journal
---

A few days ago I was a little bit concerned and I modified the player I have in [celestes.org](http://celestes.org/) (the famous [Flash Video Player](http://www.jeroenwijering.com/?item=Flash_video_Player)). Its biggest problem is that it exposes the file you want to reproduce as a parameter, so it's easy to steal the video from the website (or even worse, to hotlink it).

I tunned it so now it gets a video id and it asks the DB to get the actual video url (something like [http://videos.celestes.org/flvplayer.swf?videoid=8](http://videos.celestes.org/flvplayer.swf?videoid=8)).

I also added a "Share" button (using JavaScript, althought I would like to have implemented it in Flash) that shows the code to include on the webpage. Now I only have to count the views, group all the videos in a single page and allow ratings to have a baby YouTube :P


<a href="img/journal/videos-celestes.png" data-toggle="lightbox"><img src="img/journal/videos-celestes.png" alt="Vídeos celestes" class="img-responsive" /></a>


**Update**: ok, everything [is set up and working](http://videos.celestes.org/). Views counting, ratings and now the player knows where it is being used. I could even have a platform to upload videos and convert them to flv, but the CPU cost could have bad consequences here in Dreamhost. 