---
layout: post
title: Singleton Design Pattern
tags: [tutorial, swift]
modified: 2017-04-04
comments: true
---
The next creational design pattern that I want to write about is often debated to be an anti-pattern. It's the singleton design pattern. While I do acknowledge the pitfalls of using the singleton design pattern, there are times when it makes tasks simpler. Let's look into the singleton design pattern.
<!--more-->

The singleton design pattern ensures that only one object of a class is ever created. This creates a global state of the object in the application and hence, should be used with caution because change in one place will affect the state wherever the object is used. 

### Singleton Pattern

Creating a singleton object follows the following steps -  

* Make its constructor private
* Create a static variable to hold its shared instance.

Consider the example of a family which has only one car. The entire family will use only this car.
##### A Car Class 

{% highlight swift %}
final class Car {
    
    static let shared = Car()
    var make: String = "Tesla"
    var model: String = "Model S"
    var registrationNo: String = ""
    
    private init() {}                    // Hide the constructor
}
{% endhighlight %}

The following code demonstrates that both variables refer to the same object -

{% highlight swift %}
let momsCar = Car.shared
let dadsCar = Car.shared

print(momsCar===dadsCar)                // returns true because both objects are the same

{% endhighlight %}

Now whenever you need to access the car object, access it like so-

{% highlight swift %}
Car.shared.(the variable you want to access)
{% endhighlight %}

Stay tuned for detailed tutorials every week on design patterns!

