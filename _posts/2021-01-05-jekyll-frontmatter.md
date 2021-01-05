---
title: "Jekyll Frontmatter Generator"
date: "2021-01-05"
layout: post
---
I was archiving an old website into Markdown, to later use in Jekyll. While creating the Markdown files, I didn't worry about the frontmatter. So when it came to publish the whole thing, I noticed that without frontmatter, the files were not read by Jekyll.

Adding the frontmatter manually would have taken a while, so I decided to write a small python script to take a look at the files, figure out whether a frontmatter was already in there, and if not, read the first headline, and take that to create the frontmatter.

You can find the code at [GitHub](https://github.com/tiefpunkt/jekyll-frontmatter-generator), together with a small how-to.
