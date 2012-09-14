---
layout: post
category: posts
title: The structure of the PDX Git user group website
author: Kenneth Pullen
---
# Background

Recently I told Duke that I'd love to volunteer to help maintain the PDX Git user group website. Then I sat around and began thinking to myself:

> Self, what is this site really for? Why do we need yet another user group website?

After a while I decided that the Gitters in Portland may want a place to:

- Announce our quarterly meetups and any other special events
- Post our meetup notes for easy access
- Post notes about our presentations, and host slides, if they are available
- Keep a list of links to awesome git resources
- Post hints, tips, short articles, etc

This site is written primarily in Markdown, with a few Liquid templates floating around to put it all together. These files are crammed through Jekyll and appear on the other side on Github's servers. This means we can't make a dynamic website. You'll have to edit files on your computer and push them to github. It also means there is no official way to enforce any kind of structure.

In order to keep everything orderly I have made a decree: There shall only be four categories of posts. They are, in no particular order of importance:

- Announcements of meetups and special events
- Presentation information (notes, slides, etc)
- Notes from a meetup
- Regular blog posts, much like this one

In addition to a post's category, most posts will be connected via a tag to a specific meetup or event. There's no real structure for the tags, but I've been using the following format for meetup tags:

    <month name>-<year>-meetup

Each post is a regular file created in the _posts directory. Each file's name will follow Jekyll's post naming policy, so that the file will be noticed by Jekyll.

Each post will have a small bit of YAML categorizing and tagging it. Here's a breakdown of what each post type needs:

## Announcements
	layout: announcement
	category: announcements
	tag: <The meetup or event tag goes here>
	title: <An appropriate title goes here>

## Presentations
	layout: presentation
	category: presentations
	tag: <The meetup or event tag goes here>
	title: <An appropriate title goes here>

Heads up! Currently you'll still have to link to the actual presentation slides in the Markdown below the YAML Front Matter.

## Notes
	layout: notes
	category: notes
	tag: <The meetup or event tag goes here>
	title: <An appropriate title goes here>

The raw notes can just be pasted into the file; the notes layout shoves them into a \<pre\>, so almost no formatting will be applied. Long lines are still wrapped.

## Regular posts
	layout: post
	category: posts
	title: <An appropriate title goes here>
	author: <Your name, probably>

Heads up! The author key isn't yet used by the post layout, and it may never be used. it's still nice to see who wrote the article. You can use the `authors` key if you'd like to specify more than one author of an article:

	authors:
	 - Constable Huckabee
	 - Sheriff Noodleham

# Other stuff

There is also a file named resources.md, but I haven't really stopped to think about that yet. I suppose for now you should just add links there, and we'll sort it out.

If you'd like to add to this site, please contact Duke Leto for commit access to the github repository. Then go crazy, but please try to keep everything orderly; a clean house is a sign of something good, I'm sure.