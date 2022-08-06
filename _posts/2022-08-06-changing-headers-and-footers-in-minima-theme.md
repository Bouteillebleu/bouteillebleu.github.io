---
layout: default
title: Changing headers and footers in Minima theme
---

The previous post was about setting up this blog. Now, time to customise it a little more.

I added a blog title ("Under the Lamplight") to `index.md`, and that shows up in the top right of the Minima theme. But at the top left, and in two places at the bottom of the page, it just has the blog URL (bouteillebleu.github.io). Can we change this to something more interesting?

Let's take a look at the Minima layout we're using, `default`. [The HTML]([minima/default.html at master · jekyll/minima · GitHub](https://github.com/jekyll/minima/blob/master/_layouts/default.html)) is very simple:

```html
{% raw %}<!DOCTYPE html>
<html lang="{{ page.lang | default: site.lang | default: "en" }}">
  {%- include head.html -%}
  <body>
    {%- include header.html -%}
    <main class="page-content" aria-label="Content">
      <div class="wrapper">
        {{ content }}
      </div>
    </main>
    {%- include footer.html -%}
  </body>
</html>{% endraw %}
```

Those files aren't in `_layouts`, but are in [a directory]([minima/_includes at master · jekyll/minima · GitHub](https://github.com/jekyll/minima/tree/master/_includes)) called `_includes`. The information we're looking for is in `header.html` and `footer.html`.

From those files, we can find out:

* On the left of the header is a link which uses Jekyll's `site.title` variable.
* On the right of the header is a link which uses the `my_page.title` variable, using the title of the first page defined. In our case, that's the name of the index page.
* The top link in the footer uses `site.title` again. [This entry was removed in the Minima theme back in 2020]([Remove RSS from social icons by DirtyF · Pull Request #464 · jekyll/minima · GitHub](https://github.com/jekyll/minima/pull/464)), but for some reason is still in here as a default. Maybe Github Pages has an old copy of the theme?
* The bottom link in the footer uses `site.author.name`.

[The Jekyll docs' list of site variables](https://jekyllrb.com/docs/variables/#site-variables) doesn't list either of these variables explicitly, but the last entry - `site.[CONFIGURATION_DATA]` - does explain how you set them.

And, if we add

```yaml
title: Under the Lamplight
author: Bouteillebleu
```

to `_config.yml`, and rename the index page to something with a plainer name (such as "All posts")...

...then we get our site to look right!


### Sources used

[Setting up a GitHub Pages site with Jekyll - GitHub Docs](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll) - Github's own documentation about using Jekyll with Github pages

[Site Variables | Jekyll](https://jekyllrb.com/docs/variables/#site-variables) - Jekyll docs reference on site variables

[Configuration - Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/docs/configuration/) - Documentation from the "Minimal Mistakes" Jekyll theme about how to configure it. This is clearer than the Jekyll reference, I think, for the settings you're actually going to use when you start out.

[Why does my repository name appear as the title in my github pages site? - Stack Overflow](https://stackoverflow.com/questions/42100627/why-does-my-repository-name-appear-as-the-title-in-my-github-pages-site) - a StackOverflow question from someone else who had the same problem.

[Escaping Liquid tags in Jekyll posts](https://sarathlal.com/escape-liquid-tag-in-jekyll-posts/) - helped me figure out why the HTML for the Minima template was importing my own blog's HTML, and how to fix it.
