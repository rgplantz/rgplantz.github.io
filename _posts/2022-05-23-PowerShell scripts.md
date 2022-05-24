---
layout: post
title:  "Using PowerShell"
date:   2022-05-23 20:45:00 -0700
# categories: jekyll update
---
I've been learning how to use PowerShell, both on Windows 10 and Ubuntu 20.04. I did the figures for my books in svg, but No Starch Press wants them in pdf. It's easy to produce the pdf version using inkscape. But since I have over 100 figures, I wanted to write a script to do it for me. I thought it would be easy to find a model of how to do this online, but it wasn't. After a bit of research and some learning, I came up with a script, which I'm sharing here:

    Get-ChildItem -Filter *.svg | ForEach-Object {inkscape --export-type="pdf" $_}

I'm using Inkscape 1.2 and PowerShell 7.2.4.
