# Setup

# Liquid

Liquid is a templating language

### object
Objects tell Liquid to output predefined variables as content on a page. Use double curly braces for objects: {% raw %}{{ and }}{% endraw %}

### tags
Tags define the logic and control flow for templates. Use curly braces and percent signs for tags: {% raw %}{% and %}{% endraw %}

### filters
Filters change the output of a Liquid object. They are used within an output and are separated by a |.


# Front matter

```
---
# front matter tells Jekyll to process Liquid
---
```
YAML placed between two triple-dashed lines at the start of a file.
For Example
```
Home: 5
```

# Layout

Support Markdown and HTML

define layout. Create a default.html in _layouts folder
```
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>{{ page.title }}</title>
  </head>
  <body>
    {{ content }}
  </body>
</html>
```
use layout 
```
---
layout: default
title: Home
---
<h1>{{ "Hello World!" | downcase }}</h1>
```

# Includes
The include tag allows you to include content from another file stored in an _includes folder. Includes are useful for having a single source for source code that repeats around the site or for improving the readability.

Define include.
Same as layout but in different folder with the name _includes

Use include
```
{% raw %}
{% include navigation.html %}
{{ content }}
{% endraw %}
```

```
{% raw %}
{% if page.url == "/" %}style="color: red;"{% endif %}
{% endraw %}
```

# Data Files

Create a Data Folder _data and put the YAML file navigation.yml inside

```
- name: Home
  link: /
- name: About
  link: /about.html
```

To use it
site.data.navigation
```
<nav>
  {% raw %}
  {% for item in site.data.navigation %}
    <a href="{{ item.link }}" {% if page.url == item.link %}style="color: red;"{% endif %}>
      {{ item.name }}
    </a>
  {% endfor %}
  {% endraw %}
</nav>
```

Use one file to represents multiple items with the same format.
Easier to add new navigation items and change the HTML structure

# Assets
put css, images, js in assets folder
put _sass in root

Sass is a fantastic extension to CSS baked right into Jekyll.
Add the following in the css folder styles.scss
```
---
---
@import "main";
```
main is the main.scss file in the _sass folder


Reference the /assets/css/styles.css in the head section of the html
```
<link rel="stylesheet" href="/assets/css/styles.css">
```

# Blogging
Blogging is post in the following folder _post 
with the following format
2018-08-21-apples.md
```
---
layout: post
author: Jill
---
bah bah bah
```

Need to add an layout 
```
---
layout: default
---
<h1>{{ page.title }}</h1>
<p>{{ page.date | date_to_string }} - {{ page.author }}</p>

{{ content }}
```

The blog page will be blog.html
```
---
layout: default
title: Blog
---
<h1>Latest Posts</h1>

<ul>
  {% raw %}
  {% for post in site.posts %}
    <li>
      <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
      {{ post.excerpt }}
    </li>
  {% endfor %}
  {% endraw %}
</ul>
```

post.url the path of the post
post.title pulled from the filename
post.excert first paragraph of the content

Need to add a navigation.yml for link navigation (See the Data section)

# Collection
Collections are similar to posts except the content doesn’t have to be grouped by date.
