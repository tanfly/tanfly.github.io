---
layout: post
title:      "APIs and API Keys"
date:       2019-08-12 17:03:17 +0000
permalink:  apis_and_api_keys
---

API stands for Application Program Interface. Essentially it allows communication between two Programs in a common language. For my Rails Portfolio Project for Flatiron, I used two different APIs, one for Cloudinary image upload and one OmniAuth Facebook logins.

APIs are essentially a list of commands. When one program uses these commands, for example, when I sent a user to facebook to login via a specific url, the other program, in this case facebook, executes a bunch of programming on it’s end and sends something back via the api, usually in the form of data. When a user logs into my website via facebook, facebook returns a hash of data about the user (among other things) that you can then operate on to extract that data. APIs are essentially a pattern of requests and responses.

In the case of something like Cloudinary, the user never even sees the Cloudinary website, and, to most users, they will probably never know they are interfacing with Cloudinary when they upload images. APIs allow you to use the functionality of another program without user’s ever having to leave your app or website.

API Keys are sort of like a username or password. They are a value assigned by the service that provides the API, in my case Cloudinary and Facebook, that identifies your application and requests.

When you call the API in your code, your API key will be part of the request. This enables the service to identify you, to accept or reject your request based on the validity of your API key, and then to send back the requested data or an error if the key was invalid.

API Keys provide identification and authorization. For this reason, they should be kept secret, and the files where they are stored should be included in your gitignore file.

APIs are a great way to add functionality to your app or website without having to write a bunch of extra code or use up space for extra features.
