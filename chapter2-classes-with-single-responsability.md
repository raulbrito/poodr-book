A class should do the smallest possible useful thing, that is, it should have a single responsability.
On the domain language, look for nouns (e.g.: bycicle, gear), and see if it's possible to associate behavior.

If reusing a class that has many responsabilities, it might run the risk that a future change in another responsability might break every class that it depends on - the problem is dependency on classes that do too much.

Test if a class has single responsability. Two possibilities:
 - ask every method as a question, and see if it makes sense: "Mr. Gear, what is your ratio?"
 - describe the class without using "and" or "or".

When to change a class:
 - when the future cost of doing nothing is the same as the current cost, do nothing now.
 
Depend on behavior, not in data:
 - Hide instance variables - data might have behavior that you don't know about. Send messages to access variables, even if they seem like data.
 - hide data structures
```ruby
 class RevealingReferences
   attr_reader :wheels
   def initialize(data)
     @wheels = wheelify(data)
   end
   
   def diameters
     wheels.collect {|wheel|
       wheel.rim + (wheel.tire * 2)
     }
   end
 
   Wheel = Struct.new(:rim, :tire)
   def wheelify(data)
     data.collect {|cell|
       Wheel.new(cell[0], cell[1])
     }
   end
 end
```
    If you can control the input, pass in an useful object. Even if you don't control the input, hide the mess even from yourself!
    
Enforce Single Responsability Everywhere
 - extract extra responsability from methods:
   * expose previously hidden qualities
   * avoid need for comments
   * encourage reuse
   * easy to move to other classes
```ruby
 def diameters
   wheels.collect { |wheel| diameter(wheel) } 
 end
 def diameter
   wheel.rim + (wheel.tire * 2)
 end
```
 - isolate extra responsabilities in classes
   * and it doesn't even need to be a fully fledged class, it can also be in the context of the current class. It shows that it can be an experiment and start evolving into a own class if needed.
