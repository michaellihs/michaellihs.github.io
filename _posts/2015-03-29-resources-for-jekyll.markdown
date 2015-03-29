---
layout: post
title:  "Some helpful resources for setting up blog with Jekyll"
summary: "A collection of resources that helped me setting up my blog with Jekyll"
date:   2015-03-29 13:30:00
categories: jekyll
---

Within this blog post, I'd like to mention some resources that helped me along setting up this blog.

### Base Template

Unfortunately I cannot remember where I got the base template for my blog. I was looking for a very lightweight theme and did not want to import all the Bootstrap or Foundation stuff. Finally I came up with the structure that you can find in [my blog's Github repository][my repository].

As for the structure of the stylesheets, I tried to follow the patterns of book [Scalable and Modular Architecture for CSS][smacss] - thanks [Sebastian Helzle][seb] for the recommendation.

Since CSS is not my strength, I had to look up quite a few things. The CSS for the sticky footer (yes, it's called sticky footer even if it is not displayed on the bottom of the browser window all the time) can be found on [this website][stickyfooter].

### Inlined Icons

For me it was the first time using inlined SVGs as icons building this blog. The theme brought some of those SVGs with it. I created the one for Slideshare using the [Socicon Font][socicon] and Adobe Illustrator following [this documentation][illustratorsvg] from css-tricks. What you basically have to do is copy the svg code that Illustrator creates and use it like in the following snippet:

{% highlight html %}
<span class="icon  icon--github">
  <svg viewBox="0 0 16 16">
    <path d="... SVG code from Illustrator goes here ..."/>
  </svg>
</span>
{% endhighlight %}

You can then set the color for the icon in your css class, e.g.

{% highlight css %}
.icon > svg path {
  fill: #e8e8e8;
}
{%endhighlight %}

### Social Media Buttons

For the rendering of the social media buttons I wanted to have simple but fancy buttons I found those [codesnippets on Codepen][codepen] which I liked a lot and build them into my blog. Since the snippet came in sass and I used scss in my styles, I found this [sass to scss converter][sassscss] very useful.

Here is a nice article on [how to generate the social URLs][socialurl] with jekyll.




[my repository]:      http://github.com/michaelknoll/michaelknoll.github.io
[seb]:                http://mind-the-seb.de/blog.html
[smacss]:             https://smacss.com/
[stickyfooter]:	      http://www.cssstickyfooter.com/using-sticky-footer-code.html
[socicon]:            http://www.socicon.com/
[illustratorsvg]:     https://css-tricks.com/using-svg/
[codepen]:            http://codepen.io/ruandre/pen/howFi
[sassscss]:           http://www.sasstoscss.com/
[socialurl]:          http://zhangwenli.com/blog/2014/08/03/make-your-own-social-sharing-bar-with-jekyll/
