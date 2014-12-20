---
layout: post
title: "A Post with a Video"
description: "Custom written post descriptions are the way to go... if you're not lazy."
tags: [sample post, video]
---

<iframe width="560" height="315" src="//http://v.youku.com/v_show/id_XODUyOTczMjMy.html?f=23222055&ev=2&from=y1.3-idx-grid-1519-9909.86808-86807.2-1" frameborder="0"> </iframe>

Video embeds are responsive and scale with the width of the main content block with the help of [FitVids](http://fitvidsjs.com/).

Not sure if this only effects Kramdown or if it's an issue with Markdown in general. But adding YouTube video embeds causes errors when building your Jekyll site. To fix add a space between the `<iframe>` tags and remove `allowfullscreen`. Example below:

{% highlight html %}
<iframe width="560" height="315" src="//http://v.youku.com/v_show/id_XODUyOTczMjMy.html?f=23222055&ev=2&from=y1.3-idx-grid-1519-9909.86808-86807.2-1" frameborder="0"> </iframe>
{% endhighlight %}