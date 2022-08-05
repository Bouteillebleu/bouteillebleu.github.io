---
title: Starting Github Pages using Github Skills
date: 2022-08-05
---

Today I was looking at potential site generators to use for Github Pages. My main language is Python, so I had a look at some generators that I'd heard of, but none of them were quite what I wanted:

* [Frozen-Flask](https://pythonhosted.org/Frozen-Flask/) with [Flask-FlatPages](https://pythonhosted.org/Flask-FlatPages/) seemed the closest to my usual work (backend web development), but also required a lot of boilerplate to get started.
* [Hyde](http://hyde.github.io/) looked neat, but I couldn't find any information on theming, which is something I would like to use rather than have to design from scratch.
* [Pelican](https://docs.getpelican.com/en/latest/index.html#) also looked good, and has [themes](https://docs.getpelican.com/en/latest/themes.html)! However, getting it set up for Github Pages seems a little more complicated than I'd like.

The obvious option is [Jekyll](https://jekyllrb.com/) - it has theme support, and Github Pages supports it well - but setting up Ruby locally just to generate blog posts is also more complicated than I'd like.

Frustrated, I searched for "simple github pages blog", which pointed me at [a GitHub Learning Lab course on Github Pages](https://lab.github.com/githubtraining/github-pages). I'd not heard of GitHub Lab before, but I see it's being shut down in less than a month, which seems a pity! However, that page linked to a new option: a [GitHub Skills template for generating a Github Pages blog](https://github.com/skills/github-pages).

And that's what I've used to make this site and the first post.

## Advice for anyone else using this Skills template

I ran into a few problems while trying this, so here's my advice to anyone else trying it out.

* The README for Step 2 onwards talk about a `my-pages` branch. This is created by the workflow for Step 0 (Start), which might not start on its own.
  * If the Step 0 workflow doesn't start on its own, you can start it manually in Actions.
* If you want to use a different theme to `minima`, and you read [the Jekyll frontmatter docs](https://jekyllrb.com/docs/front-matter/) and the example there, be aware that not every theme has a `post` layout!
  * You can find out what layouts there are for the Github Pages builtin themes (the ones you can select in Settings > Pages) by looking at the repos in https://github.com/pages-themes and checking in their `_layouts` directories.
