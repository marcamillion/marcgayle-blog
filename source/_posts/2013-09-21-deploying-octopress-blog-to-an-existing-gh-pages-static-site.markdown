---
layout: post
title: "Deploying octopress blog to an existing gh-pages static site"
date: 2013-09-21 05:17
comments: true
categories: octopress github gh-pages
---

The issue I faced was that I have an <a href="http://5kmvp.com">existing static site</a> hosted on Github via `gh-pages`. That is just regular HTML/CSS/JS. It works perfectly.

But, I wanted to add an elegant Octopress blog to that same static site - so I can have both my company site & blog hosted on Github's powerful hosting platform.

This is how I pulled it off.

+ Get the folder of your static site all setup like normal. Get all the pathings right for your /img, /css, /js, etc.
+ Follow all the directions in the Octopress <a href="http://octopress.org/docs/setup/">setup</a> and <a href="http://octopress.org/docs/deploying/github/">deployment</a> guide.
+ Install the theme you want for Octopress (it is important to do this step before the rest of the steps, because everytime you install a theme it resets your index.html).
+ Follow <a href="http://octopress.org/docs/theme/template/#landing_page">these instructions</a> about moving your blog index page - make sure to update the Rakefile, per the instructions.
+ Then use these settings in your files:

`_config.yml` (you can customize all the other settings, but these worked for me)
	
	url: http://5kmvp.com
	subscribe_rss: /atom.xml
	root: /
	permalink: /blog/:year/:month/:day/:title/
	source: source
	destination: public
	category_dir: blog/categories
	
Rakefile
	
	public_dir      = "public"    # compiled site directory
	source_dir      = "source"    # source file directory
	blog_index_dir  = 'source/blog'    # directory for your blog's index page (if you put your index in source/blog/index.html, set this to 'source/blog')

Then once that is done, you copy your existing static site (with the exact structure that you setup earlier) into your `/octopress/source/` folder - so yours should look similar to <a href="https://github.com/marcamillion/5KMVP/tree/source/source">mine here</a>.

What you will notice is that now Octopress will publish to /blog (which is a subfolder called 'blog' in your 'source' folder).

Basically the way Octopress works is that at it's core, it copies everything from /source/ except for a few exceptions (all folders that start with `_`, etc.)

If you have any conflicts with your folders (e.g. if you have /img/ and Octopress has /images/) then just copy both if you don't want have to update your paths in all your HTML files. It's no big deal.

That's pretty much it.

Remember that `rake preview` and `rake generate` are your friends. Use them religiously.

If you have any issues with styling, then you may need to play around with some of the paths in the various variables in your `_config.yml` and `Rakefile` a bit. But you should't have to, because all of these values worked for me - and I did A LOT of playing around.

**Special Note: You should end up with your static site index.html in the root folder of the generated site - you can see the <a href="https://github.com/marcamillion/5KMVP/blob/source/source/index.html">source</a> here and the <a href="https://github.com/marcamillion/5KMVP/tree/gh-pages">generated version</a> here - and you should also have an octopress generated index in the `/blog/` subfolder - again...the <a href="https://github.com/marcamillion/5KMVP/blob/source/source/blog/index.html">source</a> here and <a href="https://github.com/marcamillion/5KMVP/blob/gh-pages/blog/index.html">generated version</a> here.** 

You can always just look at <a href="https://github.com/marcamillion/5KMVP/tree/source/source">my entire source to see what I did</a>.

Good luck and I hope this saves some poor soul from spending weeks trying to figure this out.