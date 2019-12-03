---
  id: 5
  uuid: "5c080e5f-29f2-4ad2-a196-dc72cc75c6b3"
  title: "How to read erlang documentation?"
  slug: "how-to-read-erlang-documentation"
  image: None
  featured: 0
  page: 0
  status: "published"
  language: "en_US"
  meta_title: None
  meta_description: None
  author_id: 1
  created_at: 1389139197979
  created_by: 1
  updated_at: 1389139197979
  updated_by: 1
  published_at: 1389139197985
  published_by: 1
  layout: "post"
  permalink: "/how-to-read-erlang-documentation/"
  published: True
  comments: True
---
While reading awesome book by [Joe Armstrong](http://en.wikipedia.org/wiki/Joe_Armstrong_(programming)), ['Programming Erlang'](http://pragprog.com/book/jaerlang2/programming-erlang), the one of the first ever exercises made me panic a little bit. The one that tells you, in occasional way, to 'Find out how to consult manual pages.'.

Running `help()` in shell didn't shed any light and consulting google wasn't straightforward so I'm just shouting out to anybody trying to find out how to read documentation or manual page – just run `erl -man <%subject%>`, like `erl -man lists` or `erl -man erl`.

Also, there're a bunch of online documentation, like, on [official site](http://erlang.org/doc/), [alternative site](http://erldocs.com/) and other stuff you can pick up at 'Where to get help' section in [http://learnyousomeerlang.com/introduction](learn you some erlang for great good), you should be checking in any case.

I would love to be black-SEO wizzard to make `erl -man whatever` to popup as first search result whether I'm trying to lookup documentation on some erlang topic (if man page exist, otherwise – straight to the doc link).

Any other ways of properly getting info on Erlang parts?
