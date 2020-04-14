---
  id: 15
  uuid: "470a543e-8368-4abd-967f-f2a9a0652373"
  title: "Readme.md as lazy persons html page"
  slug: "readme-md-as-lazy-persons-html-page"
  image: None
  featured: 0
  page: 0
  status: "published"
  language: "en_US"
  meta_title: None
  meta_description: None
  author_id: 1
  created_at: 1431566998033
  created_by: 1
  updated_at: 1431613723988
  updated_by: 1
  published_at: 1431613723990
  published_by: 1
  layout: "post"
  permalink: "/readme-md-as-lazy-persons-html-page/"
  published: True
  comments: True
---
Occasionally, working on some projects hosted on github, we put much time into creating useful & comprehensive README.md file for our project and I think you can benefit from using it to create html pages hosted on github that will be always in sync with the content.

## Issue
When you might benefit from thing I'm talking about?
For example, your README.md is magnificent & [useful](http://www.slideshare.net/michaelklishin/scalable-open-source), you have some static examples hosted on github page but there's no landing page and no connection between two. Whenever someone lands on your examples, if he knows how [github pages](https://pages.github.com/) work, he might edit the URL in his address bar & land on your repo (not everyone does & that's quite normal).
And on top of that, you don't have time/skillset to do a cool static page and will be happy with something minimal for lack of better alternative.
I turned to do this after I've seen I have different content in README.md & static page used for the folder (hosted on github pages) for statically hosted [slides project](https://github.com/sudodoki/slides) of mine.

## How to solve it?

__Turn your README.md into static page!__
Your repo is already on github, and whenever you push something to branch name `gh-pages` it's being build & published to `%username%.github.io/%reponame%` (given it's enabled in the repo's [settings](https://github.com/%username%/%reponame%/settings)). Only exception is your very own github space that resides in repo called `%username%.github.io` and will be using `master` branch to build stuff out. \[UPD 2020: you actually can now [customize](https://pages.github.com/) the branch & even tweak subfolder github pages are built from\].
Github pages use [Jekyll](jekyllrb.com) - static site generator written in Ruby. There're some catches to it - you cannot run [plugins on Github pages](http://jekyllrb.com/docs/plugins/), Github is using some custom markdown parser, but those are minor considering how useful this feature is, providing static site hosting & ability to use markdown to create content (you can run your very own blog using Jekyll or [Octopress](http://octopress.org/) built on top of it and pay noone for that). \[UPD 2020: this blog is now using jekyll\]

## 'Code' to do that
To signal Jekyll that some markdown needs processing, you add YAML syntax [FrontMatter](http://jekyllrb.com/docs/frontmatter/) in the very beginning, which can be as brief as two sets of triple dashes, separated by newline.
```
---
---
```
Learned this some time ago when was battling with Jekyll for [kottans.org](http://kottans.org) site, which now seems to be a common knowledge, marked as ProTip in the corresponding section of documentation.
But after README.md will be processed it will be output as 'README.html', which poses a minor issue. We don't want to change the name of the file (README.md will rendered by default when looking at repo page using github), but we want to be able to navigate to root path of our project and still be able to see something instead of four-oh-four page, which means we want to have `index.html` page probably.
I used something simple as static page that would be redirecting to `README.html`. There're at least 2 different ways to redirect using `<meta>` tag and couple of ways to navigate to another page using JS, so it shouldn't be of too much of a trouble. I ended with following code: 

```
<!DOCTYPE html>
<html>
<head>
  <title>Redirecting to main site</title>
  <meta charset="UTF-8">
  <meta http-equiv="refresh" content="0;url=README.html">
</head>
<body>
  Redirecting<i>↻</i>
</body>
</html>
```

And that would be pretty much everything that needed to be made in order for your README.md get 2 horizontal rulers on top (those tripple dashes added for jekyll's sake) & it's very own html representation on your github pages.

## Caveats 

#### Broken Charset on Localhost & `_layouts`
If you use [github-pages](https://github.com/github/pages-gem) gem to bootstrap jekyll locally and directly going to 'localhost:4000' URL, you might see some issues with encoding because of lack of specification of proper character encoding. This won't be a problem when pages are on Github, because Github sets `charset=utf-8` encoding using `Content-Type` header. In any case, if that might be a problem for you, you might want to add layout with proper charset. For this, you will need to create `_layouts` folder and put `default.html` with following markup:

```
<!DOCTYPE html>
<html>
<head>
  <title>These are my precious slides!</title>
  <meta charset="UTF-8">
</head>
<body>
{% raw %}  {{ content }}{% endraw %}
</body>
</html>
```

and in your README.md you will have to put 
```
---
layout: default
---
```
which will render not that pretty when looking at your github project page, but as soon as you do that step you can add all sorts of [customization and styling](http://jekyllthemes.org/) to the page.

#### Default markdown parser might work differently from Github's
In process of creating html version page for one of [my slides](http://sudodoki.github.io/slides/react-102/) it turned out that markup of 
###### ~~Strike through heading~~
isn't working in markup used in jekyll by default.
Thanks to [issue#1752](https://github.com/jekyll/jekyll/issues/1752)  in jekyll repo I was able to go over bunch of different possible engines to render markdown to find the one that worked correctly for page that used [github flavored markdown](https://help.github.com/articles/github-flavored-markdown/) (spoiler: it was `rdiscount`).
To set an engine used on your gh-pages, you will need to create  `_config.yml` file in root of your project and put 
```
markdown: rdiscount
```
into it.
That did solve the issue of. 😼

#### Nested folders & `README.md`
Every folder, especially when it's a separate entity/project, should have its own README.md to explain how/what/why of the contents. That will mean, that you will have to apply the same changes to the README's content as to the one in you project root (and add redirecting page).

## Write READMEs
Be a good person and don't just throw your stuff over the fence in the world of open source. Share your work, show you care about it & people using it, and you will get tenfold in return. Hope this small note will help you have this while spending less time. Hope it was somewhat useful. 😇

