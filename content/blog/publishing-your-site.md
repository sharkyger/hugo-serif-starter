---
title: "Publishing your site"
date: 2026-03-02T09:00:00+10:00
draft: false
description: "From local preview to a live deployment."
feature_image: "images/illustrations/reading.svg"
---

Once your content looks right locally, publishing is the easy part. This post
walks through the path from `hugo server` to a deployed site.
<!--more-->

## Preview locally

Run `hugo server` and open the address it prints. Edits reload instantly so you
can iterate on content and styling.

## Build and deploy

When you are happy, run `hugo` to build the static site into `public/`, then
upload that folder to any static host. No server or database required.
