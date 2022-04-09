---
layout: default
title: Reflecting on Ruby Reflection for Rendering RBIs
event: RubyKaigi 2020
video: https://youtu.be/OJRQAn6BfpE
date: 2020-09-04 00:00 +0000
---

As part of our adoption process of Sorbet at Shopify, we needed an automated way to teach Sorbet about our ~400 gem dependencies. We decided to tackle this problem by generating interface files (RBI) for each gem via runtime reflection.

However, this turns out to not be as simple as it sounds; the flexible nature of Ruby allows gem authors to do many wild things that make this Hard. Come and hear about all the lessons that we learnt about runtime reflection in Ruby while building `tapioca`.
