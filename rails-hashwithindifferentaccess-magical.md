---
title: Rails HashWithIndifferentAccess magical
published: true
description: 
tags: Ruby, Rails, tricks

---
![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/tyn1ny34yt50dhqi2x46.jpg)

In daily development the parameters passed to the `action` in the `Controller` when implementing business logic will be placed in the `params` object. generally we can access with 

```ruby
params[:token] #=> token_value
#or
params["token"] #=> token_value
```

You will find that the value of **key** in `params` can be access by using `Symbol` or `String`. 

Is it a bit magical? 

In fact the principle is very simple `params` have the characteristics extend from `HashWithIndifferentAccess`

```ruby
class HashWithIndifferentAccess < Hash
  #......
	def []=(key, value)
		regular_writer(convert_key(key), convert_value(value, for: :assignment))
	end
  
	# key point 
	def convert_key(key) 
	   key.kind_of?(Symbol) ? key.to_s : key
	end
	
	def self.[](*args)
		new.merge!(Hash[*args])
	end
end
```

Through the above source code analysis, it can be seen that for a `HashWithIndifferentAccess` object, when assigning it **key** is uniformly converted into **String** type (`covert_key` method). 

When a value is to be taken, the **key** of the Symbol will be forced to be converted to `String` so that the user can use **Symbol ** or **String** to take the same value.


Hope it can hlep you :)
