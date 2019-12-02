---
  id: 9
  uuid: "97471a58-6d75-48fd-a151-88ef1a259226"
  title: "TIL: pre/post are for everybody!"
  slug: "til-prepost-are-for-everybody"
  image: None
  featured: 0
  page: 0
  status: "published"
  language: "en_US"
  meta_title: None
  meta_description: None
  author_id: 1
  created_at: 1405461460081
  created_by: 1
  updated_at: 1425840697085
  updated_by: 1
  published_at: 1405461460083
  published_by: 1
  layout: "post"
  permalink: "/til-prepost-are-for-everybody/"
  published: True
---
Just a short note on discovery (which is not too much of a discovery actually): you can use *pre-* & *post-* hooks in `npm-scripts` for your own custom tasks.
So, next time you would need to run several things as part of one task, you could leverage those.

    {
      "scripts": {
	    "premyscript": "echo \"Pre stuff\"",
        "myscript": "echo \"LOL MY SCRIPT\" ",
        "postmyscript":"echo \"Post stuff\""
      }
    }

So, if we run `npm run myscript` in the folder where package.json would hold abovementioned lines, we would see something like:

    $ npm run myscript

    > npm-test@0.0.0 premyscript /home/sudodoki/Projects/npm-test
    > echo "Pre stuff"

    Pre stuff

    > npm-test@0.0.0 myscript /home/sudodoki/Projects/npm-test
    > echo "LOL MY SCRIPT"

    LOL MY SCRIPT

    > npm-test@0.0.0 postmyscript /home/sudodoki/Projects/npm-test
    > echo "Post stuff"

    Post stuff
    
   
**UPD (21/7/14):** Note on this [became part](https://github.com/npm/npm/commit/f9f58dd0f5b715d4efa6619f13901916d8f99c47) of oficial documentation. **OSS FTW**