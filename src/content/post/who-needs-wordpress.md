---
title: "Who needs WordPress? (Or how to make a personal blog in the age of 'DocOps')"
date: 2016-08-13T18:36:04-07:00
draft: true
---

Have you always wanted your own blog, but don't know where to start?

In this article, I'll explain why you want to write content in **Markdown** and use a static site generator to translate that into a plain, old HTML site that you can stick just about anywhere.

You then want to setup a pipeline to automate the process and deploy. Let's call such a thing a **DocOps Pipeline**, to be cute and catchy.

Best of all, this can be done today for **free** and without having to place ads on your blog (unless you want to, I guess).

Curious? Let's dive in...

...and if you just want to get to the **How To** steps and skip all my well thought out explanation (you monster) click [HERE](#how-to)

## Preface: Picking on WordPress

I named this article "Who needs WordPress?" because that is what most people think of when they think of a personal blog. WordPress is a **content management system** that was created in 2003, written in PHP (which I'm not digging on, we've all used it). Nothing is really "wrong" with it. [1/3 of the internet](https://w3techs.com/technologies/details/cm-wordpress/all/all) uses WordPress.

However, there are some concerns. As anyone that's tried to _roll their own_ server with WordPress, or any similar CMS technology, can tell you: you are constantly at the mercy of whatever venerability is present with it and you have to constantly stay up to date. And if you use any plug-ins, the issue compounds itself. Also, there is an admin area that controls the whole site, that is one breach away from disaster.

If you go with the **free** hosted option of WordPress.com, you avoid having to stay up to date, but your visitors are at the mercy of advertising you don't control.

The other downside is the "What you see is what you get" (WYSIWYG) editor of WordPress. You can never exactly tell it what you want. There seems to always be extra tags and garbage in the final HTML markup. As someone that **does code** for a living, I go right to the raw HTML, every single time. It just doesn't feel right _not_ to.

There _has_ to be a better way.

## Separation of Content and Style

The best plan for the preservation of what you write is a separation of the actual content from the system that delivers that content.

Why? Say you want to change the system, you have to **hope** that the old system has a way to export your data in a way that can be imported into the new system.

What if you had everything already in a format that transcends any content system. That way, in ten years, when something new comes out, you'll have a much better chance of converting to it.

It also needs to be as compact and simple as possible.

## Viva El Markdown

Markdown is a fairly simple and compact way to write content while expressing _exactly_ what you **want**. For instance, that last sentence looks like this in Markdown:

```md
Markdown is a fairly simple way to write content while expressing _exactly_ what you **want**.
```

Once you get a feel for it, you are able to write so much faster than any WYSIWYG editor would ever let you. Moreover, sites like **GitHub** and **Reddit** have it at the heart of their content entry. If you frequent either of those site, **you already know Markdown**!

Want a working example? See how this article looks in raw Markdown [HERE](https://raw.githubusercontent.com/ThomasMPorter/Blog/master/src/content/post/who-needs-wordpress.md).

## Making With The Pretty

There are quite a few technologies that can take your content in Markdown and make it into a static website:

- DocFx
- Hugo
- Sphinx

The one that makes the most sense for a blog is Hugo. It's got the most flexibility when it comes to themes and ease of use.

## How To {#how-to}

Here is how to setup a DocOps Pipeline just like the one used for this very site. Everything is using free services, but there are paid alternatives for each.

Technologies in this practical example:

- Hugo
- GitHub (free account)
- Azure Pipeline (free account)

### Setup

1. [Install Hugo](https://gohugo.io/getting-started/installing) on you local machine. The setup will be different depending on what OS you use. The link provided has their instructions.

1. [Pick a theme](https://themes.gohugo.io/) and set it up. This is a matter of preference and will start to give the site its personality.

1. Start with the "Example Site" for the theme.

1. Customize it to your liking

1. Upload it to a GitHub Repository

1. Setup an Azure Pipeline

1. Install the Hugo and GitHub Pages Publish Marketplace extensions

1. Use the following **.yml** configuration:

```yml

```

1. Make a test commit.

### Everyday Use