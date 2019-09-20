---
layout: post
title:      "Fast JSON API "
date:       2019-09-20 14:38:10 +0000
permalink:  fast_json_api
---


My most recent project for Flatiron involved an SPA with Rails API backend and Javascript frontend.

Using rails as an API meant that data within the backend needed to interface accessibly with my frontend. The data in the backend needed to be as well structured as possible to make that interfacing run as smoothly as possible.

While it is fully possible to specify which data should be rendered to JSON within the controller, (and actually, Rails makes it quite easy with render :json), the data that is output with this method is pretty messy. Again, it is entirely possible to clean up that data within the controller, but there are also gems specifically available to do this for you.

For this project I implemented Fast JSON API, a gem actually designed by Netflix. The Fast JSON API gem provides a serializer generator within Rails that supports has_many, belongs_to, and has_one relationships, all of which I utilized for my project.

With this gem I was able to utilize serialization of my data to provide a uniform and clean json response to my frontend.
I was able to specify what data I wanted to allow, and also able to easily include relationships between my models. This was crucial because I had many interwoven relationships.

My app is a world-building app, for writers or fantasy enthusiasts to write out all aspects of a world.
Users have many worlds, worlds have many regions, and each region has a plethora of details, such as terrain or climate, which belongs to them.

The cleanliness and predictable organization of this data enabled me to make clean, abstracted functions that would work across a spectrum of responses from my database.
