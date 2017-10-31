---
layout: post
title: Homestead como entorno de desarrollo profesional.
tags: 'PHP, Laravel'
thumbnail: /assets/images/uploads/Community-Manager-1099x550.png
permalink: /:year/:month/:day/:title
---
You'll find this post in your `_posts` directory. Go ahead and edit it and re-build
the site to see your changes. You can rebuild the site in many different ways, but
the most common way is to run `jekyll serve`, which launches a web server and
auto-regenerates your site when a file is updated.

To add new posts, simply add a file in the `_posts` directory that follows the
convention `YYYY-MM-DD-name-of-post.ext` and includes the necessary front matter.
Take a look at the source for this post to get an idea about how it works.

{% highlight ruby %}
def show
  @widget = Widget(params[:id])
  respond_to do |format|
    format.html # show.html.erb
    format.json { render json: @widget }
  end
end
{% endhighlight %}

<script src="https://gist.github.com/ismaeldevmw/be5afff123ac9f36c9f3177861feb40a.js"></script>

## Accessing the CMS

Your site CMS is now fully configured and ready for login!

If you set your registration preference to “Invite only,” you’ll need to invite yourself (and anyone else you choose) as a site user. To do this, select the Identity tab from your site dashboard, and then select the Invite users button. Invited users will receive an email invitation with a confirmation link. Clicking the link will take you to your site with a login prompt.

If you left your site registration open, or for return visits after comfirming an email invitation, you can access your site’s CMS at yoursite.com/admin.

Happy posting!



```
<div class="share-box">
```

```
<h5>Comparte esto:</h5>
```

```

```

```
<a class="f" href="https://www.facebook.com/sharer/sharer.php?u={{ site.url }}{{site.baseurl}}{{ page.url }}" onclick="window.open(this.href, 'mywin',
```

```
'left=20,top=20,width=500,height=500,toolbar=1,resizable=0'); return false;" ><i class="fa fa-facebook-official fa"></i><span> facebook</span></a>
```

```

```

```
<a class="t" href="https://twitter.com/intent/tweet?text={{ page.title }}&url={{ site.url }}{{site.baseurl}}{{ page.url }}" onclick="window.open(this.href, 'mywin',
```

```
'left=20,top=20,width=500,height=500,toolbar=1,resizable=0'); return false;"><i class="fa fa-twitter fa"></i><span> twitter</span></a>
```

```

```

```
<a class="g" href="https://plus.google.com/share?url={{ site.url }}{{site.baseurl}}{{ page.url }}" onclick="window.open(this.href, 'mywin',
```

```
'left=20,top=20,width=500,height=500,toolbar=1,resizable=0'); return false;" ><i class="fa fa-google-plus fa"></i><span> google</span></a>
```

```

```

```
<a class="r" href="http://www.reddit.com/submit?url={{ site.url }}{{site.baseurl}}{{ page.url }}" onclick="window.open(this.href, 'mywin',
```

```
'left=20,top=20,width=900,height=500,toolbar=1,resizable=0'); return false;" ><i class="fa fa-reddit fa"></i><span> reddit</span></a>
```

```

```

```
<a class="l" href="https://www.linkedin.com/shareArticle?mini=true&url={{ site.url }}{{site.baseurl}}{{ page.url }}&title={{ page.title }}&summary={{ page.desc }}&source=webjeda" onclick="window.open(this.href, 'mywin',
```

```
'left=20,top=20,width=500,height=500,toolbar=1,resizable=0'); return false;" ><i class="fa fa-linkedin fa"></i><span> linkedin</span></a>
```

```

```

```
<a class="e" href="mailto:?subject={{ page.title }}&amp;body=Check out this site {{ site.url }}{{site.baseurl}}{{ page.url }}"><i class="fa fa-envelope fa"></i><span> email</span></a>
```

```
</div>
```
