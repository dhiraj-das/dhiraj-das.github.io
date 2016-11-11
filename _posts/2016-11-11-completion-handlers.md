---
layout: post
title: Completion Handlers
excerpt: "Tutorial to explain how completion handlers work in swift"
tags: [tutorial, swift]
modified: 2016-11-11
comments: true
---

Completion handlers in swift are a bit confusing at first if you are not used to blocks or closures, but they are extremely useful in situations where an API request or task take some time to get completed and you specifically want something to  happen after *completion* of that task. Let us see how we can implement a completion handler in our methods.

**NOTE:** Completion handlers in swift can be compared to lambda expressions[^1] in Java. 

[^1]: <https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html>

### Completion Handler Structure

A completion handler is a closure. A completion handler usually has a signature like this. 

{% highlight swift %}
completion: (NSData?, NSURLResponse?, NSError?) -> Void
{% endhighlight %} 

This tells us that its a code block with three arguments and has a void return type. 

### Example of a method having a completion handler

{% highlight swift %}
let task = NSURLSession.sharedSession().dataTaskWithURL(URL, completionHandler: { (data, response, error) in
            if error == nil {
                // do something ...
            }
        }).resume()
{% endhighlight %}

### Writing your own completion handlers

Adding a completion method to your own methods is not difficult. It follows the same steps as writing your own method.

{% highlight swift %}
func someTaskThatTakesAWhileToComplete (aParameter : Int, completion: (success: Bool) -> Void) {
        if aParameter == 1 {
            completion(success: true)
        }else {
            completion(success: false)
        }
    }
{% endhighlight %}

Your method defines when to set the parameter *success* true or false and thus anyone using your method just needs to handle his code according to the success of your method. Thus,

{% highlight swift %}
someTaskThatTakesAWhileToComplete(45) { (success) in
            // do stuff related to failure of someTaskThatTakesAWhileToComplete
        }
        
        someTaskThatTakesAWhileToComplete(1) { (success) in
            // do stuff related to success of someTaskThatTakesAWhileToComplete
        }
{% endhighlight %}

Hope this tutorial was worth your time!

