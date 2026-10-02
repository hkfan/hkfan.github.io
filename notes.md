

Own static files
static site generator. (customize build process locally or on another server)
e.g. Jekyll or GitHub Action workflow - 

disable the Jekyll build process by creating an empty file called .nojekyll in the root of your publishing source,

Limit to 1GB Content
100GB per month
Copy site only for Educational

## Custom Workflow

configure-pages Action

```
- name: Configure GitHub Pages
  uses: actions/configure-pages@v5
```

Upload page Artifact
```
- name: Upload GitHub Pages artifact
  uses: actions/upload-pages-artifact@v4
```

Deploying Artifact
```
# ...
jobs:
  deploy:
    permissions:
      contents: read
      pages: write			# Must have write
      id-token: write			# Must have write
    runs-on: ubuntu-latest
    needs: jekyll-build			# Must be set as the id of the build step
    environment:
      name: github-pages
      url: ${{steps.deployment.outputs.page_url}}
    steps:
      - name: Deploy artifact
        id: deployment
        uses: actions/deploy-pages@v4
# ...
```

Can put Build and depoly in a single file 
```
jobs:
    build:
    depoly:
```

## Publishing Source

push to a branch - can select branch to depoly; fold can only be / or /docs
Github Actions

Must use "Github action" if contains symbolic link file

Workflow template
1. Trigger
2. Checkout
3. Build Statics site files
4. upload artifacts
5. Deploy

Delete the site by changing the source branch to None
Unpublish the site by removing the current depolyment

add a 404.html
or 404.md to indicate file not found
When using md, add the following at the front
```
---
permalink: /404.html
---
```
You can only use submodules that point to public repositories, because the GitHub Pages server cannot access private repositories.
https:// read-only URL for your submodules,

# Jekyll

Prohibuted Keywords
/node_modules
/vendor
files start with _, . or #
files end with ~

## Configuration


## Front Matters
1. Set Variables
2. Metadata - title, layout
3. In YAML format

Example
```
---
layout: post
title: Blogging Like a Hacker
---
```
---
food: Pizza
---
```

## theme
Supported out of the box theme : Architect Cayman Dinky Hacker Leap day Merlot Midnight Minima Minimal Modernist Slate Tactile Time machine
Supported other Jekyll theme hosted in Github

## Plugin
Enable by adding it in _config.yml


# To Early to know

1. Configuration a publishing source - (has template)
2. Github Action workflow - free for public
3. Jekyll Build Error
4. MIME types
5. Jekyll Theme
6. Third party CDN (Content Distribution Network)
7. Configure Pages action
8. What is the meaning of @v4 and @v5
9. Viewing workflow run history
10. Configuration in Jekyll https://jekyllrb.com/docs/configuration/
11. Front Matter
12. using site.github
13. Using other Jekyll theme hosted in Github



