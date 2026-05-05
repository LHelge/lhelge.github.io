---
title: Moving to new hosting platform
slug: new-hosting
author: LHelge
created: 2023-06-29
description: "Moving lhelge.se to GitHub Pages and generating the site with Jekyll"
image: /static/blog/jekyll.png
tags:
  - lhelge.se
  - GitHub
  - Cloudflare
  - Proton
---

This domain have housed different types of sites over the years. It started out with a [WordPress](https://wordpress.com/) blog, but lately it has been just an empty placeholder.

# Hosting
I have been using a Swedish company for both web and e-mail hosting for over a decade. Their e-mail service has started to fall behind on several areas, and also in security, not supporting MFA. I decided to move my mail to [Proton](https://proton.me/) and their Family account with support for custom domains. I have also moved my DNS-services to [Cloudflare](https://cloudflare.com), and only had my web hosting left at my old provider.

This lead to the decision to move web hosting to [GitHub Pages](https://pages.github.com/) instead which would allow me to cancel the current hosting service.

# Platform
When moving to [GitHub Pages](https://pages.github.com/) the static site generator [Jekyll](https://jekyllrb.com/) is usually the first choice due to the seamless integration. I decided to try that together with the theme [Chirpy](https://chirpy.cotes.page/) (you may recognize that page) 😜.

Let's see how that works out, but so far, Jekyll seems to be a really nice way to host a blog-like site.