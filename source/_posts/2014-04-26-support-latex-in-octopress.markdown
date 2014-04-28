---
layout: post
title: "Support LaTex In Octopress"
date: 2014-04-26 16:29:48 +0800
comments: true
categories: 
---
There are many posts introducing how to support Latex in Octopress, and how to display math formulars in web pages, bellow is what I have done.

MathJX
------
Many websites use [MathJX](www.mathjax.org) to display math symbols and formulars. MathJX is an open source JavaScript display engine for mathematics works in all browsers. Because it was writted in JavaScript, it does not require browser plugins to display math symbols, and it is indeed very attracted in developers and users' eyes.

How do Math StackExchange do?
----------------------------- 
Math StackExchange use following javascript code to config the MathJX engine:
{% highlight JavaScript linenos %}
<script type="text/x-mathjax-config">
    MathJax.Hub.Config({"HTML-CSS": { preferredFont: "TeX", availableFonts: ["STIX","TeX"], linebreaks: { automatic:true }, EqnChunk:(MathJax.Hub.Browser.isMobile ? 10 : 50) },
                        tex2jax: { inlineMath: [ ["$", "$"], ["\\\\(","\\\\)"] ], displayMath: [ ["$$","$$"], ["\\[", "\\]"] ], processEscapes: true,ignoreClass: "tex2jax_ignore|dno" },
                        TeX: {  noUndefined: { attributes: { mathcolor: "red", mathbackground: "#FFEEEE", mathsize: "90%" } }, Macros: { href: "{}" } },
                        messageStyle: "none"
                      });
</script>
<script src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS_HTML-full"></script>
{% endhighlight %}

Would markdown's format overlays with LaTex?
--------------------------------------------
Actually, yes. Some standard markdown's format does. However, Kramdown does support an additional syntax feature to support Latex, as the [ducument](http://kramdown.gettalong.org/syntax.html\#math-blocks) said.
{% highlight text %}
A math block needs to start and end on block boundaries. It is started using two dollar signs, optionally indented up to three spaces. The math block continues until the next two dollar signs(which may be on the same line or on one of the next lines) that appear at the end of a line. The content of a math block has to be valid LaTex math. It is always wrapped inside a \begin{displaymath}...\end{displaymath} environtment except if it begins with a \begin statement.

Using inline math is also easy: just surround your math content with two dollar signs, like with a math block. 
{% endhighlight %}

Overall, how to do?
-------------------
- Config the MathJX engine in each html files head as follow:
{% highlight JavaScript %}
<script type="text/x-mathjax-config">
    MathJax.Hub.Config({
        text2jax: { inlineMath: [ ["$", "$"], ["\\\\(", "\\\\)"] ], displayMath: [ ["$$", "$$"], ["\\[", "\\]"] ], processEscapes: true }
    });
</script>
<script src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS_HTML-full"></script>
{% endhighlight %}
- Change the config markdown engine to kramdown in "\_config.yml".
That's all. Let's have some exmaples.

1. Show a complex math block:
{% highlight text %}
$$
\begin{align*}
  & \phi(x,y) = \phi \left(\sum_{i=1}^n x_ie_i, \sum_{j=1}^n y_je_j \right)
  = \sum_{i=1}^n \sum_{j=1}^n x_i y_j \phi(e_i, e_j) = \\
  & (x_1, \ldots, x_n) \left( \begin{array}{ccc}
      \phi(e_1, e_1) & \cdots & \phi(e_1, e_n) \\
      \vdots & \ddots & \vdots \\
      \phi(e_n, e_1) & \cdots & \phi(e_n, e_n)
    \end{array} \right)
  \left( \begin{array}{c}
       y_1 \\
       \vdots \\
       y_n
    \end{array} \right)
\end{align*}
$$
{% endhighlight %}

$$
\begin{align*}
  & \phi(x,y) = \phi \left(\sum_{i=1}^n x_ie_i, \sum_{j=1}^n y_je_j \right)
  = \sum_{i=1}^n \sum_{j=1}^n x_i y_j \phi(e_i, e_j) = \\
  & (x_1, \ldots, x_n) \left( \begin{array}{ccc}
      \phi(e_1, e_1) & \cdots & \phi(e_1, e_n) \\
      \vdots & \ddots & \vdots \\
      \phi(e_n, e_1) & \cdots & \phi(e_n, e_n)
    \end{array} \right)
  \left( \begin{array}{c}
       y_1 \\
       \vdots \\
       y_n
    \end{array} \right)
\end{align*}
$$

2. Show an inline math:
{% highlight text %}
this is an inline math: $$ x=y+z $$.
{% endhighlight %}

this is an inline math: $$ x=y+z $$.

How about this one: \$$ x=y+z $$.

And how about this: \$\$ x=y+z $$.


