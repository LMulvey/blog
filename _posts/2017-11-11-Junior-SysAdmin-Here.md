---
layout: post
title: Junior SysAdmin
---

I've spent the last week embarking on a new adventure for me. It's one that I've looked
forward to for a while. The journey to becoming a junior *SysAdmin*. 

I try to expand my skillset whereever possible. I strive to **never stop learning** and continue to grow and learn. It's especially applicable in an industry like web development that's always changing- not only in terms of technology, frameworks, and languages, but also in terms of job roles. Many agencies now expect a web developer to wear many hats: Front-end Developer, Back-end Developer, Designer, Copywriter, and **System Administrator**. I strive to at least have a *little* knowledge in each of these roles to make myself the wearer of many hats.

# The Reluctant SysAdmin

A client was recently having a few issues with his site. When I took him on as a client, he had arranged free hosting with a friend of his. His friend had operated an Apache server part-time to issue people hosting and had some *extra space* on one of his servers. The client, wanting to keep costs low, opted for the free host. I was initially okay with this but ran into issues quickly. While developing a PHP image cropping tool that used the Imagick, I ran into an issue- Imagick wasn't enabled server-side. I contacted the friend to see if we could get it enabled. Weeks went by without a response before finally saying that they could infact enable it, and that it had been done. I went to test my tool again:

```php
Class 'Imagick' not found.
```

Sigh. So, I contact him again. Weeks go by with no response. I'm left talking to the client to discuss why this issue is happening, and why I can't get the tool working-- a tool that was in the original scope of the project and was due to be finished *months ago*. Eventually, I had my client agree to pay for proper hosting. But, having come fresh off the frustrations of needing to go through someone else to fix sever issues, I suggested that we go the route of *DigitalOcean*. I didn't have a ton of experience actually spinning up an Ubuntu sever from scratch and new I had a bit of reading to do.

I've spent the last few weeks working through [*Servers For Hackers* by Chris Fidao](https://book.serversforhackers.com/) to help guide me on my adventure. Now that the client's site is actually ported over and up-and-running, I'll share a few of my learnings:

## PM2 for process-handling

The server was working, my Node.js app was launched, and everything was great. Until the next morning. It shut down. After looking into it, I realized that issuing `npm start` from console would cause my `server.js` to shutdown as soon as I lost connection to SSH. Instead, I looked into PM2 which is a process-handling program for Ubuntu. With it, I could setup PM2 as a startup app for Ubuntu and then start my Node.js app through PM2 which runs it as a service. With this setup, the app restarts when it needs to, and if the server crashes and resets, my `server.js` is launched again by PM2.

## Express Routes

I seriously needed to read the documentation here on serving static files. My file structure was as follows:

```
/app
->/server
-->/views
-->/routes
->/public
-->/css
-->/js
```

After launching my app through PM2, I learned how `express.static` actually works and where how it finds my static files. After doing a ton of reading and wanting to throw my MacBook off my balcony, I found a solution that worked. I removed my `/server/` folder and moved my `server.js` to the main app directory, along with my `/routes/` and `/views/` folders. I then set my `express.static` to: `express.static(__dirname + '/public')` and all my static assets were properly served.

## Not The End

This is where I'm at only a few days in. It's exciting being in command of your own VPS and not having to create support tickets to fix minor issues. I'll continue to share mmy learnings as I go!



