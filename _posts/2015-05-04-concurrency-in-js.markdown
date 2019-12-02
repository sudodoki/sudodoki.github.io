---
  id: 13
  uuid: "ec79055f-f58b-4eda-ba83-00f7db58e637"
  title: "Concurrency in JS"
  slug: "concurrency-in-js"
  image: None
  featured: 0
  page: 0
  status: "published"
  language: "en_US"
  meta_title: None
  meta_description: None
  author_id: 1
  created_at: 1430752367785
  created_by: 1
  updated_at: 1431228827486
  updated_by: 1
  published_at: 1430752495953
  published_by: 1
  layout: "post"
  permalink: "/concurrency-in-js/"
  published: True
---
Recently I've been to [BostonJS](http://bostonjs.com/) at Bocoup, where [Naveed Ihsanullah](https://twitter.com/naveedi) from Mozilla shared some of the upcoming concurrency features that will come to live supposedly in about a year (and this talk took place on 30th of April 2015).

Previously, closest we had to concurrency was usage of [Web Workers](https://developer.mozilla.org/en-US/docs/Web/API/Worker), which solved some of the problems. It provided us with ability to offload heavy computations from our single threaded javascript. It was safe in terms of playing well with single threaded execution model, but involved some overhead for communication between main thread and workers, as well as imposing restrictions to what kind of code could run in those.

Looks like things are going to change. There's a [draft spec](https://docs.google.com/document/d/1NDGA_gZJ7M7w1Bh8S0AoDyEqwDdRh4uSoTPSNn77PFk/edit#heading=h.a6o4dubw5qla) "Spec: JavaScript Shared Memory, Atomics, and Locks", and [this gist](https://gist.github.com/dherman/5463054) that talks about `SharedArrayBuffer` primitive that would be concurrently accessible. You could read about motivation and roadmap in February [entry in Mozilla blog](https://blog.mozilla.org/javascript/2015/02/26/the-path-to-parallel-javascript/).

Naveed joked about bringing [deadlocks](http://en.wikipedia.org/wiki/Deadlock) & [race conditions](http://en.wikipedia.org/wiki/Race_condition) to previously safe js (which is great pun and will help make future interviews 'funnier': '- do you want to create static pages for us & validate some forms? - Yeah! - Great, tell us about concurrency & deadlocks in javascript').
I might have got previous paragraph distorted, so here's an actual comment by Naveed:
>Deadlocks are actually possible now in JavaScript. Shared memory and the associated locks, however, would potentially allow data races and new deadlocks because of synchronization. A bit different. What I meant is shared memory can be complex and JavaScript was spared that complexity in the past. Depending on how we finally choose to surface this functionality that may not be the case in the future.


It seems that API will be going through some dramatic changes over the course of next months. Naveed mentioned that on the day of the talk there was an interesting idea of looking into the way C++ handles threads & modifying the API slightly. For more details, you might want to take a look at [this draft](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2014/n4195.pdf).

Closing up was the demo of visualizing [Mandelbrot fractal](http://en.wikipedia.org/wiki/Mandelbrot_set), which used all 8 cores. Notably, it was also using [SIMD](http://en.wikipedia.org/wiki/SIMD), which made code run several times faster. The fractal demo itself was about 6x faster (using 8 cores instead of 1), than normal JS because of shared memory & threading. SIMD brought another 2.5-3.5x pefromance boost.

Such an API might be used to enable some great things in the web, as well as bring us another way to shoot ourselves in the foot.

Naveed did mention necessity of future involvement of library authors to wrap this powerful low-level primitives to bring end-users handy tools that would enable easier work, especially when it will involve VR, image processing and other heavy-computational activities that will get only more widespread as we go forward.
Oh, Naveed did mention that there was a [public indication](https://groups.google.com/a/chromium.org/forum/#!topic/blink-dev/d-0ibJwCS24) that V8 team had intention of implementing this, so let's just hope we will have this generally available in around a year.

All in all, this looks like interesting space to follow & I would definetely be looking forward to Naveed's talk on [JSCONF US 2015](http://2015.jsconf.us/speakers.html#ihsanullah).

I want to thank Naveed for taking time to review this post & provide additional details I didn't get right the first time 😼