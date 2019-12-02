---
  id: 6
  uuid: "0e33261a-a2d1-4bdb-9b7a-09c103b1456e"
  title: "Sublime: ignoring folder in Project / goto definition."
  slug: "sublime-ignoring-folder-in-project"
  image: None
  featured: 0
  page: 0
  status: "published"
  language: "en_US"
  meta_title: None
  meta_description: None
  author_id: 1
  created_at: 1389306804080
  created_by: 1
  updated_at: 1425840799229
  updated_by: 1
  published_at: 1389357819181
  published_by: 1
  layout: "post"
  permalink: "/sublime-ignoring-folder-in-project/"
  published: True
---
Just 2 quick things about Sublime I would like to share for those, who might be having these issues.

###Remove folder from project.
Say, you're NodeJS developer (or, generally speaking, using npm in your work)  and you don't want to see certain folders in your neat little project, like node_modules. You might have a question: 'How do I remove a single folder out of my project?'. I assume the answer is you don't, you just add it into ignore, I think, it's like that in JetBrains' IDEs too (at least, it used to be like that).
For that just go to Project -> Edit Project and add the following:
```
{
  "folders":
  [
    {
      "follow_symlinks": true,
      "path": "jschat",
      "folder_exclude_patterns": ["node_modules"]
    }
  ]
}
```
or any other [globbing pattern](http://www.tldp.org/LDP/GNU-Linux-Tools-Summary/html/x11655.htm) – I've seen `*` or `**` in the wild project configs, mostly.
###Goto definition on ctrl + left click 
First thing I was missing for some time after switching from JetBrains Rubymine was goto definition functionality, which was as simple, as pressing ctrl + function/class name to get to its definition.
Sublime has nice 'Goto Symbol', 'Goto Symbol in Project' and 'Goto Definition' functionality.
To use Goto definition, you can just press f12 on your keyboard. In case you're user of [Sidebar Enhancements](https://github.com/titoBouzout/SideBarEnhancements) which is really neat ST plugin, be sure to add `{ "keys": ["f12"], "command": "goto_definition" }` into 'Preferences' -> 'Key Bindings – User' to override plugins standard behavior (open file in default editor). Also, in case you prefer ctrl + click behaviour, just:
1. Go to 'Preferences' -> 'Browse Packages...'
2. Create file in 'User' folder called `Default (%Your OS name, Linux|Windows|OSX %).sublime-mousemap` . On linux system you would just
`vim ~/.config/sublime-text-3/Packages/User/Default\ \(Linux\).sublime-mousemap`  
3. Add following content 
```
[
  {
    "button": "button1",
    "modifiers": ["ctrl"],
    "command": "goto_definition"
  }
]
```
4. Save and enjoy.
It just defines that on left mouse button click (button1, when right is button2), when control key is also pressed 'Goto Definition' should be called.