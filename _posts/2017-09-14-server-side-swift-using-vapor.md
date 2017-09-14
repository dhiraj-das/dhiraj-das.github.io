---
layout: post
title: Server Side Swift using Vapor - Setup
tags: [tutorial, swift]
modified: 2017-09-14
comments: true
---
Swift has amazing potential on the server and there are a lot of third-party server side swift frameworks available. 

Some top frameworks available at the time of writing this blog are- [IBM Kitura](http://www.kitura.io/), [Vapor](https://vapor.codes/) and [Perfect](http://perfect.org/).

You should try all the frameworks and see what works best for you. You should never pick a framework on [speed](https://medium.com/@rymcol/linux-ubuntu-benchmarks-for-server-side-swift-vs-node-js-db52b9f8270b) alone, or any other single metric. Give them all a try.
<!--more-->

In this blog post I will be discussing about setting up a Vapor project and setting up a GET route.


#### Add Homebrew Tap

{% highlight shell %}
brew tap vapor/homebrew-tap
brew update
{% endhighlight %}

#### Install Vapor CLI

{% highlight shell %}
brew install vapor
{% endhighlight %}

---

With Vapor CLI installed, lets create a new Vapor project

##### Step 1:
{% highlight shell %}
vapor new blogger
{% endhighlight %}

![new project](https://preview.ibb.co/jyL3w5/Vapor_New_Project.png)

##### Step 2:

{% highlight shell %}
vapor build
{% endhighlight %}

If you are on macOS, you would want to create an xcode project :heart_eyes:

{% highlight shell %}
vapor xcode
{% endhighlight %}

![create xcode project](https://preview.ibb.co/kKtyw5/Screen_Shot_2017_09_14_at_4_36_25_PM.png)
 
---

#### Setting up a GET route

In the main.swift file inside the Run folder, add these lines of code at the bottom of the file. 

{% highlight swift %}
drop.get("hi") { request in
    return "Hello, world!"
}
{% endhighlight %}

Now, save the file and quit xcode.

{% highlight shell %}
vapor run
}
{% endhighlight %}

type this in your browser 'http://localhost:8080/hi' -

You should see Hello, world!

---

That's it for this blog post. In the next blog post, i'll discuss about configuring POST routes and integrating PostgreSQL with your vapor project.
