# README

## Sitemap

```bash
.
├── README.md
├── _config.yml
├── _layouts
│   ├── default.html
│   └── post.html
├── _posts
│   ├── 2023-06-05-welcome-to-jekyll.markdown
│   └── ...
├── _includes
│   ├── header.html
│   └── footer.html
├── docs
│   ├── Club_Overview.md
│   ├── Membership_Guidelines.md
│   ├── Documentation
│   │   ├── Meeting_01.md
│   │   ├── Meeting_02.md
│   │   └── ...
│   ├── Tutorials_and_Training_Materials
│   │   ├── Getting_Started
│   │   │   ├── Guide_01.md
│   │   │   └── ...
│   │   ├── Workshop_Materials
│   │   │   ├── Workshop_01.md
│   │   │   └── ...
│   │   └── External_Resources.md
│   ├── Projects_and_Research
│   │   ├── Project_01
│   │   │   ├── README.md
│   │   │   └── ...
│   │   ├── Project_02
│   │   │   ├── README.md
│   │   │   └── ...
│   │   └── Research_Papers
│   │       ├── Paper_01.md
│   │       └── ...
│   ├── CTFs_and_Challenges
│   │   ├── Past_Challenges
│   │   │   ├── Challenge_01.md
│   │   │   └── ...
│   │   ├── Upcoming_CTFs.md
│   │   └── Practice_Challenges
│   │       ├── Challenge_01.md
│   │       └── ...
│   ├── Tools_and_Software
│   │   ├── Open_source_Tools
│   │   │   ├── Tool_01.md
│   │   │   └── ...
│   │   └── Custom_Tools
│   │       ├── Tool_01.md
│   │       └── ...
│   ├── Discussion_and_Ideas
│   │   ├── Idea_Tracker.md
│   │   └── Discussions.md
│   └── Miscellaneous
│       ├── Events.md
│       └── Links_and_References.md
├── assets
│   ├── css
│   │   ├── main.scss
│   ├── js
│   │   ├── main.js
│   └── img
│       └── logo.png
└── index.md
```

### Folders

1. The `_layouts` folder is where templates are defined for this website
2. The `_posts` folder is where blog posts would go
3. The `_includes` folder can contain snippets of code to include in layouts
4. The `assets` folder is for:
   1. CSS
      1. **Note** that Jekyll uses SCSS for its style files, which is a superset of `CSS` that includes features like variables and nesting.
   2. JavaScript
   3. images
5. `index.md` file at the root of the repository is the content for the main page of the website.
   1. Any .md files in the root of the repository will be converted into pages on the website.
6. `_config.yml` file for site settings:
   1. This includes things like
   2. The site name
   3. Author name
   4. The theme being used

## Github Pages

One of the great things about Jekyll is its simplicity. To create a new page, all you have to do is create a new HTML or Markdown file.

Just specify the branch and the directory (usually `main` and `/docs`, or `main` and `root`) from where GitHub Pages should build your site.

It is worth mentioning that while Jekyll is the easiest to use with GitHub Pages (since it's supported directly), you can still use other static site generators like Hugo or MkDocs. You would just need to build the site locally and commit the generated static files.

## GitHooks

### pre-commit

```bash
#!/bin/sh
# pre-commit

if git rev-parse --verify HEAD >/dev/null 2>&1
then
    against=HEAD
else
    # Initial commit: diff against an empty tree object
    against=4b825dc642cb6eb9a060e54bf8d69288fbee4904
fi

# Redirect output to stderr.
exec 1>&2

# Check for TODO comments
if ! git diff-index --cached --quiet $against -- '**/*.js' '**/*.jsx' '**/*.ts' '**/*.tsx' '**/*.html' '**/*.css' '**/*.scss' '**/*.md' '(exclude)package-lock.json' '(exclude)yarn.lock'; then
    echo "To be committed:"
    git diff --cached -- '**/*.js' '**/*.jsx' '**/*.ts' '**/*.tsx' '**/*.html' '**/*.css' '**/*.scss' '**/*.md' '(exclude)package-lock.json' '(exclude)yarn.lock'
    if git diff --cached --name-only -z $against | xargs -0 grep -n 'TODO'; then
        echo 'ERROR: Commit contains TODO'
        exit 1
    fi
fi

# Normal exit
exit 0
```

### Setup .hooks

```bash
# Run this command once to set up the hooks
git config core.hooksPath .hooks
```
