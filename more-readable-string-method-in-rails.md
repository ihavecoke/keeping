---
title: More readable string method in rails
published: true
description: 
tags: ruby, rails, tricks
---
![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/zysoijq8bica6qvyy5fz.jpg)

First look at the code:

```ruby
Rails.env.development? #=> true

```

If rails run at local development environment it will return `true`

Why can call the `development?` method directly on the `Rails.env` object? 

The point is that you can use **?** suffix at method very simple, let's show you source code.

```ruby
module ActiveSupport
  class StringInquirer < String
    def method_missing(method_name, *arguments)
      if method_name[-1] == "?"
        self == method_name[0..-2]
      else
        super
      end
    end
  end
end
```

In fact `Rails.env` is an` ActiveSupport::StringInquirer` instance object. the `ActiveSupport::StringInquirer` object extends the `method_missing` of the `String` class. 

Mainly compare the string before `?` with the string itself

```ruby
name = ActiveSupport::StringInquirer.new("mixbo")
name.mixbo? #=>true

'mixbo?'[0..-2] #=> 'mixbo' 
'mixbo' == 'mixbo' #=>true
```

Hope it can help you :)
