---
  id: 11
  uuid: "a24cc839-9f0f-43e9-8301-0172bbe62684"
  title: "ui.router: absolutely@nothing"
  slug: "ui-router-absolutelynothing"
  image: None
  featured: 0
  page: 0
  status: "published"
  language: "en_US"
  meta_title: None
  meta_description: None
  author_id: 1
  created_at: 1405633025548
  created_by: 1
  updated_at: 1425839945920
  updated_by: 1
  published_at: 1425839802806
  published_by: 1
  layout: "post"
  permalink: "/ui-router-absolutelynothing/"
  published: True
---
###Absolutely adressing views in angular-ui-router.

Something not many people had to leverage while working with [ui-router](http://angular-ui.github.io/ui-router/site/) is its ability to use [absolute/relative addressing](https://github.com/angular-ui/ui-router/wiki/Multiple-Named-Views#view-names---relative-vs-absolute-names).
Behind the scenes every ui-view gets assigned absolute path. You can easily find [source for figuring out '@'-name for view](https://github.com/angular-ui/ui-router/blob/3e06565f5d5e1973c168116e905bd2fb569abcc6/src/viewDirective.js#L299) by randomly poking around code or stepping over debugger (that happened in my case).
This minor thing might come off handy some day when you're dealing with irregular outlet structure or different view hierarhies, that are supposed to be sharing same views. 
In my case it was a task of having sidebar, which could have 2 different possible configurations & hierarchies – depending on different parts of the app – with state specific widget embedded into it. Naming my ui-view `plug@sidebar` in different outlets & addressing those in my state definition object worked like a charm.
It might be a bit risky relying on internal API, so don't forget to have tests for that & have proper dependency management. 😸
