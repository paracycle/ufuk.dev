---
layout: default
title: The Curious Case of the Bad Clone
event: RailsConf 2021
video: https://youtu.be/ok45gtFuMO8
date: 2021-05-19 00:00 +0000
---

On Sept 4th 2020, I got pinged on a revert PR to fix a 150% slowdown on the Shopify monolith. It was a two-line change reverting the addition of a Sorbet signature on a Shop method, implicating Sorbet as the suspect.

That was the start of a journey that took me through a deeper understanding of the Sorbet, Rails and Ruby codebases. The fix is in Ruby 3.0 and I can sleep better now.

This talk will take you on that journey with me. Along the way, you will find tools and tricks that you can use for debugging similar problems. We will also delve into some nuances of Ruby, which is always fun.
