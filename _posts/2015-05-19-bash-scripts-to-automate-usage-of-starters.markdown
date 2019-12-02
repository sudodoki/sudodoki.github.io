---
  id: 16
  uuid: "b4e94379-01cd-4041-affc-b592ab21d85b"
  title: "Bash scripts to automate usage of starters/boilerplates"
  slug: "bash-scripts-to-automate-usage-of-starters"
  image: None
  featured: 0
  page: 0
  status: "published"
  language: "en_US"
  meta_title: None
  meta_description: None
  author_id: 1
  created_at: 1432012740727
  created_by: 1
  updated_at: 1432017245395
  updated_by: 1
  published_at: 1432017005795
  published_by: 1
  layout: "post"
  permalink: "/bash-scripts-to-automate-usage-of-starters/"
  published: True
---
# ![](/content/images/2015/05/scaffolding.jpg) 

There are a lot of different starters & boilerplate projects out there, especially for the frameworks/systems that are not tied up by conventions. From those quite widespread right now I would name angular (see [angular seeds](https://docs.google.com/spreadsheets/d/1r8rJy2Q5p5QORYKcye93UECwOlSgFL24c5fyF7dqhaM/pubhtml#)) and [react](https://github.com/enaqx/awesome-react#boilerplates) to have quite a bit of those, each of which might bring some interesting ideas/tools/paradigms to the table.

There're some minor things I would love to see less when people are providing instructions on using their seed/starter for starting project
1) Forgetting to specify `--depth 1` as argument to `git clone`. Omitting that argument will mean cloning whole tree with history, which gets you extra overhead on space & waste more time to start the project (especially on slow bandwidth or for projects that have gone a loooong way and have hundreds/thousands of commits under the belt).
2) Suggesting using same git - not hinting on how to specify new remote url, or get rid of previous history, which caused the folder size to bloat (especially with conjunction with #1), etc.

To simplify this flow in case you're quite frequent user, you might want to have some handy aliases. For some time I occasionally ran
`git clone https://github.com/%some-boilerplate-project%.git my-bp-project && cd $_ && rm -rf .git` to get me a plain folder from which I could start building up, which ended up living in my alias section of .zshrc file.

So following are the examples of zshrc aliases (which should work on bash/sh with minor modifications (at some point I put it into separate template.sh file with `#!env sh` shebang and code did work although there were some changes regarding [regex matching](http://stackoverflow.com/a/22539067/1976857)). Here, we have `template` alias which will use provided git URL (be it ssh/https ones you would copy from github/bitbucket or github username/reponame pair) & name of the folder (with fallback to boilerplate name itself as folder name) that it will proceed to clone to specified folder, remove original `.git` folder and init empty git repo. It will also save the git url to the `~/.last_template` file (plain text file), which can be leveraged by `last-template` alias, which reuses last provided template and basically is template with default value of last used boilerplate provided via `~/.last_template` file.
```bash
cloneCleanup() {
  # $1 - $GITREMOTE
  # $2 - $FOLDER_NAME
  echo "Will be setting up $GITREMOTE in $FOLDER_NAME"
  # Clone last commit, remove git folder, init empty git repo, save the last used template
  if git clone --depth 1 $1 $2 && cd $_ && rm -rf .git && git init && echo $1 > ~/.last_template ; then
    echo "Ready to work."
  else
    echo "Something went wrong."
  fi
}
scaffoldGithub() {
  # Script to scaffold project based on github repo
  GITREMOTE=$1
  # Handle username/reponame case
  if [[ "$1" =~ ^[A-Za-z0-9_-]+\/[A-Za-z0-9_-]+$ ]]
  then
    GITREMOTE="https://github.com/$1.git"
  fi
  # capture PROJECT_NAME part of git link (right before .git)
  REGEX="([A-Za-z0-9_-]+).git$"
  [[ "$GITREMOTE" =~ $REGEX  ]];
  PROJECT_NAME="${match}"
  # use provided folder name with fallback to project name
  FOLDER_NAME="${2:-$PROJECT_NAME}"
  cloneCleanup $GITREMOTE $FOLDER_NAME
}
simplifiedScaffoldGithub() {
  # Script to reuse last used template saved in ~/.last_commit
  GITREMOTE="`cat ~/.last_template`"
  # Throw in case user forgets to put in folder
  : ${1?"Usage: last-template foldername"}
  FOLDER_NAME="$1"
  cloneCleanup $GITREMOTE $FOLDER_NAME
}

alias template=scaffoldGithub
alias last-template=simplifiedScaffoldGithub
``` 

To add alias you will need to add them to one of your environment config files. I usually have put them into [.(ba|z)shrc](https://gist.github.com/sudodoki/b0d9e9320969aad65011) files.
After adding aliases & reloading the environment (`source ~/.zshrc` in my case) you can use them.
Sample usages:
```
template https://github.com/kriasoft/react-starter-kit.git my-killer-startup-secret-product
template roman01la/f-react-kit
last-template glorious-app
```


At some point I almost had published this as a separate tool (just a set of executable shell scripts & installation script to link those to `usr/bin`) on github, because only thing I've seen doing something similar was [scaffoldinpy](https://github.com/hex7c0/scaffoldinpy). Although it might be I just didn't look hard enough for this.
Will appreciate feedback on this.