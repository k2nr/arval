# Arval

Arguments and Return value VALidator for ruby

## Installation

Add this line to your application's Gemfile:

    gem 'arval'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install arval

## Usage

```ruby
require 'arval'

class Klass
  include Arval

  def_validator(:multiple_i) do
    a.is_a Numeric
    b.is_a Numeric
    return_value.is_a Integer
  end

  def multiple_i(a, b)
    (a * b).to_i
  end

  def_validator(:wrong_method) do
    a.is_a String
    b.is_a String
    return_value.is_a Integer
  end

  def wrong_method(a, b)
    a + b
  end
end

# enable validator
Arval.enable

k = Klass.new
# passes 2 Numeric value and returns Integer
# this call satisfies what validator defines
k.multiple_i(1.2, 1.3)
#=> 1

# wrong arguments
k.multiple_i("abc", "def")
#=> raise error

# return value doesn't match validator definition
k.wrong_method("abc", "def")
#=> raise error
```

## Contributing

1. Fork it ( http://github.com/<my-github-username>/arval/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
