---
layout: post
title: "Share Code Snippets"
date: 2014-04-29 21:32:59 +0800
comments: true
categories: 
---
Ways to share code snippets in Octopress:

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


