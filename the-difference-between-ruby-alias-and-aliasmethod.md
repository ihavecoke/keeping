---
title: The difference between Ruby alias and alias_method
published: true
description: 
tags: Ruby, Ticks
---
![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/xw9mkm972psx5f61xugs.jpg)

In some open source **ruby** projects  you may see similar `alias` and `alias_method` methods. what are the specific use of these two methods? how are these two methods different? let's look at the following code:

```ruby
#alias
class User
  def full_name
    puts "Mixbo"
  end
  alias name full_name
end
User.new.name #=>Mixbo

#alias_method
class User
  def full_name
    puts "Mixbo"
  end
  alias_method :name, :full_name
end
User.new.name #=> Mixbo
```

The above examples all output the "Mixbo" string before renaming the `full_name` in the `User` class. from this example alone we can't see the difference between the two methods continue:

```ruby
#alias_method
class User
  def full_name
    puts "Super Mixbo"
  end
  def self.rename
    alias_method :name, :full_name #==> Note that alias_method is used here
  end
end

class Mixbo < User
  def full_name
    puts "Mixbooooo"
  end
  rename
end
Mixbo.new.full_name #=> "Mixbooooo"


#alias
class User
  def full_name
    puts "Super Mixbo"
  end
  def self.rename
    alias :name :full_name #==> Note that alias is used here
  end
end

class Mixbo < User
  def full_name
    puts "Mixbooooo"
  end
  rename
end
Mixbo.new.name #=> 'Super Mixbo'

```

From the above example we can see that when there is an inheritance relationship between classes. `alias` will not affect its subclasses. related `alias_method` will find the closest method of the same name in its subclass to operate (for example, `full_name` above)

### So `alias` and `alias_method`

  1. Can give an alias to a method

  2. `alias` is generally valid when the source code is interpreted by the compiler

  3. `alias_method` is generally valid when the code is running

Generally I use `alias_method` a little more.

Hope it can help you :)
