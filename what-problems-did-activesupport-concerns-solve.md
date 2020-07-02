---
title: What problems did active_support concerns solve?
published: true
description: 
tags: Ruby, Rails
---
![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/65670e41o57mxgrj2zq0.jpg)

In the Rails project some of the most commonly used methods are extracted and generally placed in the corresponding concerns directory. generally different concern files are stored in these directories. a file is a module for example:

```ruby
module UserPlan
  extend ActiveSupport::Concern
  included do 
    belongs_to :plan
  end
  class_method do 
    def	cached_all_plan 
      #bala bala
    end
  end
end
```

Note that the module `extend ActiveSupport::Concern` is used in this module. we will explore its benefits and why this module exists.

Let's start with the following example:

```ruby
module Foo
  def self.included(base)
    base.class_eval do
      def self.method1
        ...
      end
    end
  end
end

module Bar
  def self.included(base)
    base.method1
  end
end

class Host
  include Foo # The Foo module was introduced because the Bar module depends on it
  include Bar # Bar reference is to call its method1 method
end
```

If you want to use the `method1` method in the `Host` class, you must refer to the `Bar` module but the `Bar` module depends on the `Foo` module. 

Did you find any problems? the `Host` class does not care about the `Foo` module but in order to call the `method1` method when the `Bar` is included. you have to Introduce the `Foo` module.

There is an improved code along the above logic:

```ruby
module Bar
  include Foo
  def self.included(base)
    base.method1
  end
end
class Host
  include Bar
end
```

The `Host` only cares about the reference of `Bar` so the `Foo` module is put in the `Bar`. It seems that there is no problem but when you implement the running code, you will find that the code cannot run. 

In the included hook method of the `Bar` module the base object points to the `Host` and the include `Foo` in `Bar` will put `method1` on the instance object of `Bar`. when the instance object of the Host calls `method1`, it will throw a method not found exception

How to do it?

```ruby	
require 'active_support/concern'
module Foo
  extend ActiveSupport::Concern
  included do
    def self.method1
      ...
    end
  end
end

module Bar
  extend ActiveSupport::Concern
  include Foo

  included do
    self.method1
  end
end

class Host
  include Bar 
end
```

By referring to `ActiveSupport::Concern` to solve the problem of interdependence between modules and modules.

The comparison found that the code is much simpler and the call is also very convenient. the readability of the code has also become very good and very clear. now `ActiveSupport::Concern` is quite widely used and many good gems will be used. after all It was put in the **ActiveSupport** Gem.



Hope it can help you :)
