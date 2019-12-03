---
  id: 10
  uuid: "1675ae7d-de51-4b9c-aad7-a7a5a652325b"
  title: "Grunt.log.write('Huh'['nocomma'])"
  slug: "grunt-log-writehuhnocomma"
  image: None
  featured: 0
  page: 0
  status: "draft"
  language: "en_US"
  meta_title: None
  meta_description: None
  author_id: 1
  created_at: 1405594554071
  created_by: 1
  updated_at: 1405594601164
  updated_by: 1
  published_at: None
  published_by: None
  layout: "post"
  permalink: "/grunt-log-writehuhnocomma/"
  published: False
  comments: True
---
How does ` grunt.log.write('Debug: '['yellow']);` works?
https://github.com/epeli/underscore.string/blob/1e465ac17bdb896f1b540ab52d88e86eef7033d6/test/strings.js#L133-L143 this?
https://github.com/gruntjs/grunt-legacy-log/blob/master/index.js#L149-L160 this?
```
String.prototype.yellow = "YELLOW"
"YELLOW"
''['yellow']
"YELLOW"
```