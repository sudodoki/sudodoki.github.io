---
  id: 7
  uuid: "6c7db4fb-5599-4f8d-ac4d-2d8857c4339c"
  title: "The day I stopped worrying about quicksort"
  slug: "the-day-i-stopped-worrying-about-quicksort"
  image: None
  featured: 0
  page: 0
  status: "published"
  language: "en_US"
  meta_title: None
  meta_description: None
  author_id: 1
  created_at: 1391456805774
  created_by: 1
  updated_at: 1425840778967
  updated_by: 1
  published_at: 1391456805778
  published_by: 1
  layout: "post"
  permalink: "/the-day-i-stopped-worrying-about-quicksort/"
  published: True
---
### Sort like you mean it
Yep, I did read about quicksort for quite few times, mostly when I was just learning how to program and was solving all kind of algorithmic challenges. I did think that I understand it, but I never fully grokked it, even though I could say 'it recursively divides array into subsets and sort those' and had some working Pascal code that did it (or at least I thought it did).

For time being I just left this matter aside and it didn't bother me, since implementing your own sorting is not a kind of problem you should be solving as a webdeveloper.

Nevertheless, insight came to me when I saw implementation of QuickSort in Erlang:

```
  qsort([]) -> [];
  qsort([Pivot|T]) ->
    qsort([X || X <- T, X < Pivot])
    ++ [Pivot] ++
    qsort([X || X <- T, X >= Pivot]).
```

If you can read this snippet, then no more explanations needed, otherwise, here they are line-by-line:
1. When we pass empty array to `qsort` function we get back an empty array.
2. When we pass non-empty array to `qsort` first element (or *head* of the list, if you prefer, having all other parts to be *tail*) is being set as a pivot. 
3. `[X || X <- T, X < Pivot]` this creates a list, that is subset of *tail* elements, which are less than Pivot value (`X <- T, X < Pivot` is a [Generator expression](http://learnyousomeerlang.com/starting-out-for-real#list-comprehensions) with guard clause). Then we pass it as an argument to recursive qsort call.
5. `[X || X <- T, X >= Pivot]` gets us the list of all elements that are equal or bigger than a Pivot and we do the same stuff as with lesser part of the list
4. We add output of #3 & #5 with Pivot, thus setting Pivot to it justly deserved place (every element to the left is less that Pivot, every element to the right is equal or bigger than Pivot).
This way every call to qsort with non-empty array means getting the index of single element and initiating a 2 chain of recursive calls, which maps to idea of [D&C](http://en.wikipedia.org/wiki/Divide_and_conquer_algorithm) neatly.

And this was it. That was my aha-moment.

I did put up a JS version of this, which is listed next:
```
  function quicksort(array) {
    // to dereference initial array
    var copy = JSON.parse(JSON.stringify(array))
    if (copy.length <= 1) {return copy}
    var randomIndex = Math.floor(Math.random() * copy.length),
        // selecting pivot & removing it from initial array
        pivot = copy.splice(randomIndex, 1),
        // getting all the elements which are less than / equal to pivot
        lesserHalf = copy.filter(function(el){return el <= pivot})
        // getting all the elements which are bigger than pivot
        biggerHalf = copy.filter(function(el){return el > pivot })
    // I would love to hear why this wouldn't work withoug closure
    return (function (lesserHalf, pivot, biggerHalf) {
      return [].concat(quicksort(lesserHalf), pivot, quicksort(biggerHalf))
    })(lesserHalf, pivot, biggerHalf)
  }
```
Hope comments and above explanation is good enough to figure out, what's going on here.

### Make me see it!
To be somehow more visual here's a visualization using [d3.js](http://d3js.org/) for array of 10 elements.
<iframe src="http://sudodoki.github.io/d3-quicksort-visualize/" width='720' height="500" frameborder="0"></iframe>


### Yep, I wanted to make a point
I did find a very [neat & well commented version](https://gist.github.com/paullewis/1981455) of in-place quicksorting (the version I came up with spawns array for each call & `filter` spawns new array as well) impelemented in JS.


Yep, in-place version is much less memory consuming, but FP style, in my opinion, is easier to comprehend. Thus I would encourage everybody to go out and read something about FP, which can bring a lot to the table of your everyday development. For example, [JavaScript Allongé](https://leanpub.com/javascript-allonge/read) if you want it to be JS related.