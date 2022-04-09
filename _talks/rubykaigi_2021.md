---
layout: default
title: Demystifying DSLs for better analysis and understanding
event: RubyKaigi 2021
video: https://youtu.be/Ms7_PrryvMM
slides: https://speakerdeck.com/ufuk/demystifying-dsls-for-better-analysis-and-understanding
date: 2021-09-09 00:00 +0000
---

The ability to create DSLs is one of the biggest strengths of Ruby. They allow us to write easy to use interfaces and reduce the need for boilerplate code. On the flip side, DSLs encapsulate complex logic which makes it hard for developers to understand what's happening under the covers.

Surfacing DSLs as static artifacts makes working with them much easier. Generating RBI/RBS files that declare the methods which are dynamically created at runtime, allows static analyzers like Sorbet or Steep to work with DSLs. This also allows for better developers tooling and as some kind of "DSL linter".
