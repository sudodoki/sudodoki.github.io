---
  id: 4
  uuid: "4fd97646-6aeb-4b8f-a509-1ef69e6d05d7"
  title: "hsl2rgb(), no Math, please"
  slug: "hsl2rgb-no-math-please"
  image: None
  featured: 0
  page: 0
  status: "published"
  language: "en_US"
  meta_title: None
  meta_description: None
  author_id: 1
  created_at: 1388081995109
  created_by: 1
  updated_at: 1425840820727
  updated_by: 1
  published_at: 1388188511231
  published_by: 1
  layout: "post"
  permalink: "/hsl2rgb-no-math-please/"
  published: True
  comments: True
---
###Hue, saturation, and lightness — hsl

>Color names aside, web colors have always been red-green-blue biased, be that through hex codes or explicit RBG (or RGBa). Although mildly less straightforward (especially if your brain is trained to break down colors into red, green and blue), HSL can actually be more intuitive because it gives you direct control over the aspects of a color’s shade rather than its logical ingredients.
> — <cite>[htmldog post](http://www.htmldog.com/guides/css/advanced/colors/)</cite>

There's more to hsl, be sure to read article cited. Basically it boils down to hue defining angle on color [circle](http://www.workwithcolor.com/hsl-color-picker-01.htm) having boundaries of 0°—360°, saturation, which defines how grayish (0% for totally gray and 100% to get all possible flashiness) color is and lightness 0%-100% defining how dark-bright color should be (with 50% being default).

I learned about this when I was looking for the way to do simple yet nicely looking color animation and learned that css can do other [things](http://www.w3.org/TR/css3-color/), apart from hex, rgb(a) and string names — like `currentColor` and deprecated css2 system colors. 

Although I did hear about this system, I never bothered to learn the formulas to convert values from hsl2rgb, and even after seing working code snippet didn't catch the idea offhand, though [wiki](https://en.wikipedia.org/wiki/HSL_and_HSV#Converting_to_RGB) did clarify the algorithm. Judge for yourself: <a class="jsbin-embed" href="http://jsbin.com/EWOlEZut/1/embed?js,output">JS Bin</a><script src="http://static.jsbin.com/js/embed.js"></script>

###Okay, so where's my mathless conversion?
First of, why bother? You might run into need to deal with color conversions if you're manipulating canvas data directly, setting each pixels red, green and blue channels, or you're in need of displaying colors using different systems. 

In first case you will probably be better off with some sort of math manipulation, because way I'm describing is rather **unperfomant** (jsPerf test I ran were 3 — Chrome — to 10 — FF — times slower).

Your solution may be just like the one I mentioned earlier, or you can use internal mechanism of your browser. These next lines:
```javascript
var el = document.createElement("div");
el.style.color = "hsl(100, 20%, 20%)";
console.log(el.style.color); // -> will output "rgb(47, 61, 40)"
```
will give you the idea where I'm heading with this.
I did read some specs and toyed around with devtools to find some sort of semiprivate API to handle color conversion, but all the `getRGBColorValue` or `RGBColor` BOMs didn't do lot for me.
So I did use the initial finding for conversion. The outcome of this is next function:
<a class="jsbin-embed" href="http://jsbin.com/OBOKUPuK/2/embed?js,output">JS Bin</a><script src="http://static.jsbin.com/js/embed.js"></script>

Some may point out the best thing about this function is [JSdoc](http://en.wikipedia.org/wiki/JSDoc). I decided to go with [self-defining function](http://stackoverflow.com/questions/19085395/self-defining-functionalso-called-lazy-function-definition-when-using-function) just to lessen the overhead of constantly creating DOM elements (thought they aren't being rendered).
After fooling around some more I found interesting behaviour connected with svg's, they behaved differently on my Chrome (v. 30 & 31) – color seems to convert to regular hex instead of rgb() string, but FF seems to output regular rgb(whatever) stuff. See the <a class="jsbin-embed" href="http://jsbin.com/EJAgaqO/2/embed?js,output">JS Bin</a><script src="http://static.jsbin.com/js/embed.js"></script> for output.

Actually, you can create any string that represents color in one of the systems, like hex, rgb, hsl, and returning uniform result, though don't know a lot of use cases for that.

If you asking yourself why you read this post, I would suggest you to use this as a witty response to a question 'how to transcode hsl2rgb without single math function'. In other case, be sure to get your hands dirty with some  [formulas](http://stackoverflow.com/questions/2353211/hsl-to-rgb-color-conversion/17002040). 

