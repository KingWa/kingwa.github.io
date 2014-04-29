---
layout: post
title: "Share Code Snippets"
date: 2014-04-29 21:32:59 +0800
comments: true
categories: 
---
Ways to share code snippets in Octopress:

Use the pygment's highlight
---------------------------
The syntax is: \{% highlight language linenos %} code \{% endhighlight %}


Simply use markdown
-------------------
To produce a code block in Markdown, simply indent every line of the block by at least 4 spaces or 1 tab.


Backtick Code Blocks
--------------------
Syntax:
    ``` [language] [title] [url] [link text] [linenos:false] [start:#] [mark:#,#-#]
    code snippet
    ```

For example, bellow:
{% highlight text %}
``` 
int main(int argc, char* argv[])
{
    printf("%s\n", "Hello, world!");
    return 0;
}
```
{% endhighlight %}
shows:
``` 
int main(int argc, char* argv[])
{
    printf("%s\n", "Hello, world!");
    return 0;
}
```
{% highlight text %}
``` c  
int main(int argc, char* argv[])
{
    printf("%s\n", "Hello, world!");
    return 0;
}
```
{% endhighlight %}
shows:
``` c  
int main(int argc, char* argv[])
{
    printf("%s\n", "Hello, world!");
    return 0;
}
```
{% highlight text %}
``` c "Hello World.cpp" mark:3 
int main(int argc, char* argv[])
{
    printf("%s\n", "Hello, world!");
    return 0;
}
```
{% endhighlight %}
shows:
``` c "Hello World.cpp" mark:3 
int main(int argc, char* argv[])
{
    printf("%s\n", "Hello, world!");
    return 0;
}
```


