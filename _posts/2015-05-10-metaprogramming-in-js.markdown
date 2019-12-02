---
  id: 14
  uuid: "7cb00be4-8668-4d1d-8dd7-e44c1adbafaf"
  title: "Metaprogramming in JS"
  slug: "metaprogramming-in-js"
  image: None
  featured: 0
  page: 0
  status: "draft"
  language: "en_US"
  meta_title: None
  meta_description: None
  author_id: 1
  created_at: 1431227591129
  created_by: 1
  updated_at: 1478554060493
  updated_by: 1
  published_at: None
  published_by: None
  layout: "post"
  permalink: "/metaprogramming-in-js/"
  published: False
---
[Metaprogramming](https://en.wikipedia.org/wiki/Metaprogramming) is not the word too frequently used in JS community (or at least, in those part I was around) historically. Having some Ruby background, I could tell that metaprogramming is a powerful technic that can help you produce terse and flexible code and given some shifts in ES itself in last few years, wanted to a) take a look at what metaprogramming could be usefult for, b)vocalize some ideas that were around for quite some time, c) make people use stuff, which will mean that browser vendors would be interested in supporting this.

## Bits of Ruby, here and there
>I have found that meta-programming is largely the domain of library APIs. Often you won't use much of it directly when creating an end-user application. But you can be sure, the many gems your application depends upon do use it extensively. Rails is a perfect example. It uses a great deal of Ruby's meta-programming chops to make all that Rails magic possible.
http://stackoverflow.com/a/13550631/1976857

DSL,
ActiveRecord
attr_accessors
Dynamic optimizations
`method_missing`

---

Design time tranformations:
Babel-macros
sweet.js
http://www.slideshare.net/tshemsedinov/metaprogramming-with-javascript


I have found that meta-programming is largely the domain of library APIs. Often you won't use much of it directly when creating an end-user application. But you can be sure, the many gems your application depends upon do use it extensively. Rails is a perfect example. It uses a great deal of Ruby's meta-programming chops to make all that Rails magic possible.
http://stackoverflow.com/a/13550631/1976857

String logger, for console/browser

React JSX. for render using Proxy to create dynamic stuff.

```
import h from 'virtual-dom/h';

export default function(tagName, props, ...children) {
  return h(tagName, props, children);
}
```
и добавлять в начале файлов c JSX:
```
/** @jsx jsx */
import jsx from './jsx';
```

http://blog.thoughtram.io/angular/2015/05/03/the-difference-between-annotations-and-decorators.html