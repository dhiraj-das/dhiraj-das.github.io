---
layout: post
title: Builder Design Pattern
tags: [tutorial, swift]
modified: 2017-03-24
comments: true
---
The first creational design pattern that I would like to discuss is the builder design pattern. This design pattern comes extremely handy when you want to create different variants of an object while avoiding constructor pollution. Useful when there could be several flavors of an object or when there are a lot of steps involved in creation of an object.
<!--more-->

Let me give you an example of how constructor pollution or **telescoping constructor anti-pattern**[^1] looks like-

{% highlight swift %}
init(noOfRooms: Int, noOfBathrooms: Int, hasBalcony: Bool, color: UIColor)
{% endhighlight %}

[^1]: <http://stackoverflow.com/a/1953567/6653777>

As you can see, the number of constructor parameters can quickly get out of hand and it might become difficult to understand the arrangement of parameters. Plus, this parameter list could keep on growing if you would want to add more options in future. This is called telescoping constructor anti-pattern. A total no-no.

### Builder Pattern

This problem can be solved by the builder pattern. Its simple- 

* Create a class for your entity which accepts its builder in its constructor
* Create a builder class for your entity created above

Let us assume we want to create a home object. A home would normally have properties like no of rooms, no of bathrooms, its color, etc.
##### The Home Class 

{% highlight swift %}
class House {
    fileprivate var color: UIColor
    fileprivate var noOfRooms: Int
    fileprivate var noOfBathrooms: Int
    fileprivate var hasBalcony: Bool
    
    init(builder: HouseBuilder) {
        color = builder.color
        noOfRooms = builder.noOfRooms
        noOfBathrooms = builder.noOfBathrooms
        hasBalcony = builder.hasBalcony
    }  
}
{% endhighlight %}

##### The HomeBuilder Class

{% highlight swift %}
class HouseBuilder {
    fileprivate var color: UIColor = UIColor.white
    fileprivate var noOfRooms: Int
    fileprivate var noOfBathrooms: Int = 1
    fileprivate var hasBalcony: Bool = false
    
    init(noOfRooms: Int) {
        self.noOfRooms = noOfRooms
    }
    
    func set(color: UIColor) -> HouseBuilder {
        self.color = color
        return self
    }
    
    func set(noOfBathrooms: Int) -> HouseBuilder {
        self.noOfBathrooms = noOfBathrooms
        return self
    }
    
    func addBalcony() -> HouseBuilder {
        hasBalcony = true
        return self
    }
    
    func build() -> House {
        return House(builder: self)
    }
}
{% endhighlight %}

That's it!!

Now whenever you need a home object just write this-

{% highlight swift %}
var myHouse: House? = nil
myHouse = HouseBuilder(noOfRooms: 2)
            .set(color: .red)
            .addBalcony()
            .set(noOfBathrooms: 3)
            .build()
{% endhighlight %}

setting the required object property as you wish and then calling **.build()**

Nifty ain't it!

Stay tuned for detailed tutorials every week on design patterns!

