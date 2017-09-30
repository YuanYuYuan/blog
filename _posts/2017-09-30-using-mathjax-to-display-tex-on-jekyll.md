---
title: "Using MathJax to display TeX on Jekyll"
header:
  teaser: /assets/images/unsplash-3.jpg
  image: /assets/images/unsplash-3.jpg
  caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
categories:
  - Jekyll
tags:
  - Jekyll
  - TeX
mathjax: true
---

Sometimes we may need to some math equations on posts, 
using LaTeX is the best way but not works on markdown,
so we have to import additional tool to deal with it.

A recommended way is using MathJax, 
which is an open-source JavaScript display engine for LaTex, MathML, AsciiMath, 
and it works in all modern browsers.


This is the [official document of MathJax](http://docs.mathjax.org/en/latest/index.html), 
and the source [mathjax](https://github.com/mathjax/MathJax).

## Usage on Jekyll

To use MathJax in CDN(Coneten Delivery Network) mode is very easy.

Just add the following tag in the markdown and it will trigger cdnjs automatically.

```html
<script type="text/javascript" async
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>
```

And for avoiding adding this annoying tag every time, 
one can add this scripts.html to folder __\_includes__.

```liquid
{% raw %}{% if page.mathjax %}
<script type="text/javascript" async
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>
{% endif %}{% endraw %}
```

Then we just need to add __mathjax:true__ at the YAML Front Matter of the post.

```yaml
title: "Using MathJax to display TeX on Jekyll"
header:
  teaser: /assets/images/unsplash-3.jpg
  image: /assets/images/unsplash-3.jpg
  caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
categories:
  - Jekyll
tags:
  - Jekyll
  - TeX
mathjax: true
```


For example, 

```tex
\\begin{align}
    \dot{x}&=Ax+Bu \\\
    y&=Cx+Du
\\end{align}
```
\\begin{align}
    \dot{x}&=Ax+Bu \\\
    y&=Cx+Du
\\end{align}
