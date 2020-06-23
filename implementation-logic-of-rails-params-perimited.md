---
title: Implementation logic of Rails Params Perimited
published: true
description: 
tags: Ruby, Sourcecode
---
![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/ba11n6opuevgcqmqj1u1.jpg)

In Rails `Controller#action`, get the parameters passed by the user to the server, and store in the DB there will be a special operation `params.require(:product).permit(:name,:desc)`

#### Why need to call the `permit` method

Imagine a scenario where you want to develop an api interface for receiving json data returned by a third party and creating it in a database.

```ruby
params= {user:{nickname: 'mixbo', email: 'lb563@foxmail.com', admin:true}}

class UsersController < ApplicationController
  def	create
    @user = User.create params[:user]
  end
end
```

As you can see from the above code, the `params` sent from the third-party interface includes a field `admin` This is a very dangerous operation.

And permit is to mark some allowed fields and check whether the permitted flag is included before saving to the database.



#### Implementation of Params#permit

The specific implementation is placed in the `ActiveSupport::StrongParameter` module

```ruby
module ActionController
  class Parameters
    def permit(*filters)
      params = self.class.new
      #..bala bala
      params.permit!
    end

    def permit!
      each_pair do |key, value|
        Array.wrap(value).each do |v|
          v.permit! if v.respond_to? :permit!
        end
      end
      @permitted = true
      self
    end

    def permitted?
      @permitted
    end
  end
end
```

You can see from the code above. when calling the `permit!` method on the `params` object. will set the `@permitted` of the params object to true

Before `params` is saved to the database, `active_record` will first check whether the parameters in `params` are approved by `permit`. The relevant source code is as follows:

```ruby
def sanitize_for_mass_assignment(attributes)
  if attributes.respond_to?(:permitted?)
    raise ActiveModel::ForbiddenAttributesError if !attributes.permitted?
    attributes.to_h
  else
    attributes
  end
end
```

The attributes passed to the `sanitize_for_mass_assignment` method are `params` objects. The method will first determine whether `params` exists in the permitted? method. 

If the `params` object can respond to the `permitted?` method, the `to_h` method is called.



Hope it can help you :)
