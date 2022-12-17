# metaprogramming

In Ruby, metaprogramming is the ability to write code that can manipulate and define other code at runtime. This is achieved through the use of special methods and techniques, 

Metaprogramming can be a powerful tool for making your code more flexible and reusable, but it can also be complex and difficult to understand, especially for beginners.

Metaprogramming is writing code that writes code during runtime to make your life easier.

Here is an example of metaprogramming in Ruby:

``` class MyClass
  def self.define_method(method_name)
    define_method(method_name) do
      puts "Hello from #{method_name}"
    end
  end
end

MyClass.define_method(:my_new_method)
MyClass.new.my_new_method # => "Hello from my_new_method" 

```


In this example, we define a define_method class method on the MyClass class. This method takes a method name as an argument and uses the define_method method to dynamically define a new instance method with the given name. We then use this method to define a new my_new_method instance method on the MyClass class and call it to see the result.

As you can see, metaprogramming in Ruby allows us to write code that can manipulate and define other code at runtime. This can be useful for creating reusable code libraries, building DSLs (domain-specific languages), and more. However, it's important to use metaprogramming carefully and only when necessary, as it can make your code difficult to understand and maintain.


define_method: This method allows you to define a new method at runtime. For example, you can use define_method to create methods with names that are determined at runtime, or to create methods that have different behavior based on some condition.

```
class MyClass
  def self.define_method_based_on_param(method_name, &block)
    define_method(method_name, &block)
  end
end

MyClass.define_method_based_on_param("say_hello") do
  puts "Hello"
end 
```

MyClass.new.say_hello # outputs "Hello"
method_missing: This method is called whenever a method is called on an object that does not have a corresponding method defined. You can use method_missing to implement custom behavior for undefined methods, such as creating methods on the fly or delegating method calls to another object.
```
class MyClass
  def method_missing(method_name, *arguments, &block)
    if method_name.to_s.start_with?("say_")
      puts method_name.to_s.split("_").last.capitalize
    else
      super
    end
  end
end

MyClass.new.say_hello # outputs "Hello"
```
send: This method allows you to call a method with a given name on an object, passing in arguments if necessary. You can use send to dynamically invoke methods on an object, which can be useful in situations where the name of the method is determined at runtime.

```
class MyClass
  def say_hello
    puts "Hello"
  end
end

method_name = "say_hello"
MyClass.new.send(method_name) # outputs "Hello"

```

class_eval and instance_eval: These methods allow you to execute code in the context of a class or instance, respectively. You can use them to dynamically modify the behavior of a class or instance by adding or changing methods, instance variables, and so on.

```
class MyClass
  def self.add_method(method_name, &block)
    self.class_eval do
      define_method(method_name, &block)
    end
  end

  def add_instance_method(method_name, &block)
    self.instance_eval do
      define_method(method_name, &block)
    end
  end
end

MyClass.add_method("say_hello") do
  puts "Hello from a class method"
end

my_obj = MyClass.new
my_obj.add_instance_method("say_hello") do
  puts "Hello from an instance method"
end

MyClass.new.say_hello # outputs "Hello from a class method"
my_obj.say_hello # outputs "Hello from an instance method"

```
These are just a few examples of meta programming in Ruby. There are many other techniques and methods available for manipulating and generating code at runtime.
