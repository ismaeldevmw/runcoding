---
layout: post
title: Homestead como entorno de desarrollo profesional.
tags: Laravel
thumbnail: /images/uploads/Community-Manager-1099x550.png
---
You'll find this post in your `_posts` directory. Go ahead and edit it and re-build
the site to see your changes. You can rebuild the site in many different ways, but
the most common way is to run `jekyll serve`, which launches a web server and
auto-regenerates your site when a file is updated.

To add new posts, simply add a file in the `_posts` directory that follows the
convention `YYYY-MM-DD-name-of-post.ext` and includes the necessary front matter.
Take a look at the source for this post to get an idea about how it works.

<script src="https://gist.github.com/ismaeldevmw/be5afff123ac9f36c9f3177861feb40a.js"></script>

## njecting Analytics Snippets {#injecting-analytics-snippets}

Often you want to inject JavaScript snippets into all pages of your site, either in the`<head>`or at the end of the`<body>`tag.

Most analytics providers, retargeting services, and A\/B testing services will give you an HTML snippet and ask you to add it to every page on your site.

Netlify lets you do this without having to pollute the source code for the site with production specific analytics snippets.

From the site settings page, find the “Custom scripts” section in “Post processing” and click “Edit”. Then give your script a name and paste the script body \(including any`<script>`tags, etc\).

Netlify lets you pick between injecting the scripts in before the closing`</head>`tag or before the closing`</body>`tag.

Note, scripts injected in this way will also show up on the`password`protection screen. This means you can easily verify that your analytics scripts are correctly configured without having to remove the password when your site is still under development.





